<template>
  <div>
    <!-- SOURCE -->
    <!-- <div ref="printMe" style="padding: 10px; background: #f5da55">
      <h1 style="color: #000; ">Print me!</h1>
    </div>-->
    <div ref="capture" class="m1" style="display: inline-block; padding: 8px;">
      <qrcode-vue :value="value" :size="size" level="H"></qrcode-vue>
    </div>
    <br>
    <button @click="print">Clonar</button>
    <br>
    <br>
    <!-- OUTPUT -->
    <img :src="output">
  </div>
</template>

<script>
import QrcodeVue from "qrcode.vue";
export default {
  data() {
    return {
      value: "1",
      size: 600,
      output: null
    };
  },
  methods: {
    async print() {
      const el = this.$refs.capture;
      // add option type to get the image version
      // if not provided the promise will return
      // the canvas.
      const options = {
        type: "dataURL",
        scale: 20
      };
      var canvas = await this.$html2canvas(el, options);
      //console.log(canvas);
      var element = document.createElement("a");
      element.setAttribute("href", canvas);
      element.setAttribute("download", "prueba.png");

      element.style.display = "none";
      document.body.appendChild(element);

      element.click();

      document.body.removeChild(element);
    }
  },
  components: {
    QrcodeVue
  },
  mounted() {
    //this.print();
  }
};
</script>
<style>
.m1 div canvas {
  width: 100px !important;
  height: 100px !important;
}
</style>
