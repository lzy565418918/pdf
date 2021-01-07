<template>
  <div>
    <canvas
      v-for="page in pdfList"
      :id="'the-canvas' + page"
      :key="page"
    ></canvas>
  </div>
</template>
<script>
import PDFJS from "pdfjs-dist";
const pdfjsLib = require("pdfjs-dist");
// pdf二进制base64数据
import pdfdata from "./data";
export default {
  data() {
    return {
      pdfDoc: null,
      pdfList: 0,
    };
  },
  mounted() {
    this.initThePDFJSLIB();
    let url = pdfdata.data;
    // console.log(url);
    this.loadFile(url);
  },
  methods: {
    // 初始化pdfjs
    initThePDFJSLIB() {
      pdfjsLib.GlobalWorkerOptions.workerSrc = require("pdfjs-dist/build/pdf.worker.js");
    },
    _renderPage(num) {
      this.pdfDoc.getPage(num).then((page) => {
        let canvas = document.getElementById("the-canvas" + num);
        let ctx = canvas.getContext("2d");
        let dpr = window.devicePixelRatio || 1;
        let bsr =
          ctx.webkitBackingStorePixelRatio ||
          ctx.mozBackingStorePixelRatio ||
          ctx.msBackingStorePixelRatio ||
          ctx.oBackingStorePixelRatio ||
          ctx.backingStorePixelRatio ||
          1;
        let ratio = dpr / bsr;
        let viewport = page.getViewport(
          screen.availWidth / page.getViewport(1).width
        );
        canvas.width = viewport.width * ratio;
        canvas.height = viewport.height * ratio;
        canvas.style.width = viewport.width + "px";
        canvas.style.height = viewport.height + "px";
        ctx.setTransform(ratio, 0, 0, ratio, 0, 0);
        let renderContext = {
          canvasContext: ctx,
          viewport: viewport,
        };
        page.render(renderContext);
        if (this.pdfList > num) {
          this._renderPage(num + 1);
        }
      });
    },
    loadFile(base64Str) {
      window.console.log(base64Str, "base64Str");
      pdfjsLib
        .getDocument({
          // atob将base64转成流文件
          ///data对象可以换成url
          data: window.atob(base64Str),
          // cMapUrl: "https://cdn.jsdelivr.net/npm/pdfjs-dist@2.0.943/cmaps/",
          cMapPacked: true,
        })
        .then((pdf) => {
          this.pdfDoc = pdf;
          this.pdfList = this.pdfDoc.numPages;
          this.$nextTick(() => {
            this._renderPage(1);
          });
        });
    },
  },
  components: {},
};
</script>
<style>
canvas {
  display: block;
  border-bottom: 1px solid black;
}
</style>