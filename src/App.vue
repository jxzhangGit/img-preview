<template>
  <Previewer
    :images="images"
    width="100px"
  />
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Previewer from "./components/Previewer/index.vue";

@Options({
  components: {
    Previewer,
  },
})
export default class App extends Vue {
  images = [
    'https://img8.ddove.com/upload/20200627/152152572583.jpg',
    'https://img8.ddove.com/upload/20200627/152152978159.jpg',
    'https://img8.ddove.com/upload/20200627/152153415941.jpg',
    'https://img8.ddove.com/upload/20200627/152155208751.jpg',
    'https://img8.ddove.com/upload/20200627/152155646203.jpg',
    'https://img8.ddove.com/upload/20200627/152159299376.jpg',
    'https://img8.ddove.com/upload/20200627/152201339760.jpg',
    'https://img8.ddove.com/upload/20200627/152200869879.jpg',
    'https://img8.ddove.com/upload/20200627/152157825109.jpg',
    'https://img8.ddove.com/upload/20200627/152156750946.jpg',
    'https://img8.ddove.com/upload/20200627/152152572583.jpg',
    'https://img8.ddove.com/upload/20200627/152152978159.jpg',
    'https://img8.ddove.com/upload/20200627/152153415941.jpg',
    'https://img8.ddove.com/upload/20200627/152155208751.jpg',
    'https://img8.ddove.com/upload/20200627/152155646203.jpg',
    'https://img8.ddove.com/upload/20200627/152159299376.jpg',
    'https://img8.ddove.com/upload/20200627/152201339760.jpg',
    'https://img8.ddove.com/upload/20200627/152200869879.jpg',
    'https://img8.ddove.com/upload/20200627/152157825109.jpg',
    'https://img8.ddove.com/upload/20200627/152156750946.jpg',
  ];
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
