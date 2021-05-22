<template>
  <div id="app">
    <Header></Header>
    <div class="canvas">
      <canvas ref="can" width="500" height="700"></canvas>
    </div>
    <SideBar></SideBar>
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
  mounted() {
    const ref = this.$refs.can;
    const canvas = new fabric.Canvas(ref);
    const rect = new fabric.Rect({
      fill: "red",
      width: 20,
      height: 20,
    });
    canvas.add(rect);
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
