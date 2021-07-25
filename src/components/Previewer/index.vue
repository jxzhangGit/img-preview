<template>
  <div>
    <div
      class="item"
      v-for="(url, index) in images"
      :style="itemStyle"
      :key="`image${index}`"
    >
      <div
        class="pic-box"
        :style="{ backgroundImage: `url('${url}')` }"
        @click="showPreviewEvent(index + 1)"
      ></div>
    </div>
    <ImgPreviewOverall
      :picListUrl="images"
      :show="showPreview"
      :order="previewIndex"
      @closePreview="closePreviewEvent"
    />
  </div>
</template>

<script lang="ts">
import { Vue, Options } from "vue-class-component";
import ImgPreviewOverall from "./ImgPreviewOverall.vue";
@Options({
  props: {
    images: { type: Array },
    width: { type: String, default: "250px" },
    gutter: { type: String, default: "10px" },
  },
  components: {
    ImgPreviewOverall,
  },
})
export default class Previewer extends Vue {
  readonly images!: string[];
  readonly width: string = "250px";
  readonly gutter: string = "10px";
  showPreview = false;
  previewIndex = 0;
  get itemStyle() {
    return {
      width: this.width,
      padding: this.gutter,
    };
  }
  showPreviewEvent(index: number) {
    this.previewIndex = index;
    this.showPreview = true;
  }
  closePreviewEvent() {
    this.showPreview = false;
  }
}
</script>

<style lang="less" scoped>
.item {
  display: inline-block;
  position: relative;
  box-sizing: border-box;
  .pic-box {
    background: #f6f6f6 no-repeat center;
    background-size: cover;
    padding-bottom: 100%;
    position: relative;
  }
}
</style>