# image-preview
图片组预览组件，基于vue，ts, less
![image](https://github.com/jxzhangGit/img-preview/blob/master/demo_show/show.jpg)

## 使用方法
```JavaScript
    import Previewer from "./components/Previewer/index.vue";
    <Previewer
        images="images"
        width="100px"
    />
```

## 参数

|参数|说明|类型|默认值|
|:-|:-:|:-:|-:|
|images|图片数组（必填）|string[]|-|
|width|小图宽度|string|'200px'|
|gutter|小图间距|string|'10px'|

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
