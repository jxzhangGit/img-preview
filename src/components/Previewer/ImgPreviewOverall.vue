<template>
  <div class="img-preview-overall" @click="closePreview($event)" v-show="show">
    <ul class="img-preview-list">
      <template v-for="(item, index) in picListUrl">
        <li v-if="index === imgIndex - 1" :key="index">
          <img :src="item" alt="image preview error" class="preview-cont" />
        </li>
      </template>
    </ul>
    <ul class="img-list-dots preview-cont" v-if="picListUrl.length > 1">
      <li
        :class="{
          dot: true,
          'dot-active': imgIndex === 1,
          'preview-cont': true,
        }"
        @click="changeIndex(1)"
      >
        1
      </li>
      <span v-if="ellipsisFront">...</span>
      <li
        v-for="i in dotLists"
        :key="i"
        :class="{
          dot: true,
          'dot-active': imgIndex === i,
          'preview-cont': true,
        }"
        @click="changeIndex(i)"
      >
        {{ i }}
      </li>
      <span v-if="ellipsisBack">...</span>
      <li
        v-if="true"
        :class="{
          dot: true,
          'dot-active': imgIndex === picListUrl.length,
          'preview-cont': true,
        }"
        @click="changeIndex(picListUrl.length)"
      >
        {{ picListUrl.length }}
      </li>
    </ul>
    <div class="prev preview-cont" @click="imgIndex--" v-show="imgIndex > 1">
      &lt;
    </div>
    <div
      class="next preview-cont"
      @click="imgIndex++"
      v-show="imgIndex < picListUrl.length"
    >
      &gt;
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Options } from "vue-class-component";
import { Prop, Watch } from "vue-property-decorator";
// @Component
@Options({
  props: {
    circulation: {type: Boolean, default: false},
    order: {type: Number, default: 1},
    picListUrl!: {type: Array},
    show: {type: Boolean, default: false},
  }
})
export default class Preview extends Vue {
  circulation!: boolean;
  order!: number;
  picListUrl!: Array<string>;
  show!: boolean;
  imgIndex: number = this.order;
  ellipsisFront: boolean = this.picListUrl.length > 10;
  ellipsisBack: boolean = this.picListUrl.length > 10;
  dotLists: Array<number> = [];
  changeIndex(index: number): void {
    this.imgIndex = index;
  }
  created() {
    if (this.picListUrl.length <= 9 && this.picListUrl.length > 2) {
      for (let i = 2; i < this.picListUrl.length; i++) {
        this.dotLists.push(i);
      }
    }
  }
  @Watch("show", { immediate: true })
  onShowChanged(val: number, oldVal: number) {
    this.imgIndex = this.order;
  }

  @Watch("imgIndex", { immediate: true })
  onImgIndexChanged(val: number, oldVal: number) {
    if (this.picListUrl.length > 9) {
      if (val - 4 > 1) {
        this.ellipsisFront = true;
      } else {
        this.ellipsisFront = false;
        this.dotLists = [];
        for (let index = 2; index < 9; index += 1) {
          this.dotLists.push(index);
        }
      }
      if (val + 4 < this.picListUrl.length) {
        this.ellipsisBack = true;
      } else {
        this.ellipsisBack = false;
        this.dotLists = [];
        for (
          let index = this.picListUrl.length - 7;
          index < this.picListUrl.length;
          index += 1
        ) {
          this.dotLists.push(index);
        }
      }
      if (this.ellipsisFront && this.ellipsisBack) {
        this.dotLists = [];
        for (let index = val - 3; index <= val + 3; index += 1) {
          this.dotLists.push(index);
        }
      }
    }
  }
  closePreview(e: any) {
    if (e.target.className.indexOf("preview-cont") === -1) {
      this.$emit("closePreview");
    }
  }
}
</script>

<style lang="less" scoped>
ul,
li {
  margin: 0;
  padding: 0;
}
li {
  list-style: none;
}
.img-preview-overall {
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  left: 0;
  top: 0;
  z-index: 9999;
  .img-preview-list {
    width: 80%;
    height: 100%;
    margin: 0 auto;
    position: relative;
    li {
      left: 0;
      right: 0;
      height: 100%;
      margin: 0 auto;
      img {
        position: absolute;
        display: block;
        max-width: 100%;
        max-height: 100%;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-50%);
      }
    }
  }
  .img-list-dots {
    display: flex;
    height: 2rem;
    max-width: 50%;
    margin: 0 auto;
    justify-content: center;
    align-items: center;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 1rem;
    bottom: 20px;
    padding: 0 10px;
    background-color: rgba(100, 100, 100, 0.6);
    .dot {
      display: block;
      line-height: 1rem;
      white-space: nowrap;
      margin: 0 0.2rem;
      width: 1rem;
      height: 1rem;
      font-size: 0.5rem;
      text-align: center;
      font-weight: 700;
      border-radius: 50%;
      color: rgba(255, 255, 255, 1);
      background-position: 3px -343px;
      cursor: pointer;
    }
    .dot-active {
      background-color: rgba(255, 255, 255, 1);
      color: rgb(255, 73, 10);
    }
    span {
      line-height: 1rem;
      color: #fff;
    }
  }
  .prev,
  .next {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    height: 100px;
    line-height: 100px;
    font-size: 10vw;
    &:hover {
      cursor: pointer;
      color: rgb(255, 255, 255);
    }
  }
  .prev {
    left: 1%;
  }
  .next {
    right: 1%;
  }
}
</style>