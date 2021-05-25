<template>
  <div id="app">
    <Header></Header>
    <div class="canvas" @click="resize($event)">
      <canvas ref="can" width="500" height="700"></canvas>
    </div>
    <SideBar
      :resizedFontSize="resizedFontSize"
      :selectedFontFamily="selectedFontFamily"
      :changedText="changedText"
      @resized="resizeHandler"
      @inputChange="addText"
    ></SideBar>
  </div>
</template>

<script>
import { fabric } from "fabric";
import SideBar from "./components/SideBar";
import Header from "./components/Header";

export default {
  name: "App",
  components: {
    SideBar,
    Header,
  },
  data() {
    return {
      ref: null,
      canvas: null,
      resizedFontSize: null,
      selectedFontFamily: "",
      changedText: "",
    };
  },
  mounted() {
    this.ref = this.$refs.can;
    this.canvas = new fabric.Canvas(this.ref);
  },
  methods: {
    addText({ text, size, font, line }) {
      var newText = new fabric.IText(text, {
        left: Math.floor(Math.random() * (300 - 1 + 1)) + 1,
        top: Math.floor(Math.random() * (600 - 1 + 1)) + 1,
        fontFamily: font,
        lineHeight: line,
        fill: "#333",
        fontSize: size,
        objecttype: "text",
      });
      this.canvas.add(newText);
    },
    resizeHandler(attributes) {
      let currentObj = this.canvas.getActiveObject(this.canvas.item(0));
      if (currentObj) {
        if (attributes.type == "size") {
          currentObj.set("fontSize", attributes.value);
        } else if (attributes.type == "line") {
          currentObj.set("lineHeight", attributes.value);
        } else if (attributes.type == "text") {
          currentObj.set("text", attributes.value);
        } else if (attributes.type == "font") {
          currentObj.set("fontFamily", attributes.value);
        }
        this.canvas.requestRenderAll();
      }
    },
    // change the font size on scaling
    resize() {
      let vm = this;
      this.canvas.on("object:scaling", function (event) {
        if (event.target.fontSize) {
          vm.resizedFontSize = (
            event.target.fontSize * event.target.scaleX
          ).toFixed(0);
        }
      });
      this.canvas.on("mouse:up", function (event) {
        if (event.target) {
          vm.selectedFontFamily = event.target.fontFamily;
          vm.changedText = event.target.text;
          vm.resizedFontSize = (
            event.target.fontSize * event.target.scaleX
          ).toFixed(0);
        }
      });
    },
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
  background-color: #eee;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.canvas-container {
  background-color: white;
  border: 1px solid #b7b7b7;
  margin: 0 auto;
  top: 50px;
}
.canvas {
  max-width: 1000px;
}
input,
label {
  display: block;
}
</style>
