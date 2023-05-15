<template>
  <div>
    <div
      ref="capture"
      class="m1"
      style="background:red;  display: inline-block; padding: 8px;"
    >Código QR entregado
      <br>
      <br>
      <qrcode-vue :value="value" :size="size" level="H"></qrcode-vue>
    </div>
    <br>
    <br>
    <button @click="downloadVisualReport()">Referencia</button>
  </div>
</template>
<script>
import QrcodeVue from "qrcode.vue";
import html2canvas from "html2canvas";

export default {
  name: "Generador",
  data() {
    return {
      value: "1",
      size: 600
    };
  },
  methods: {
    //Vue equivalent for document.getElementById
    showCaptureRef() {
      //console.log(this.$refs.capture);
      return this.$refs.capture;
    },
    // Screen capture function
    /*downloadVisualReport() {
      let vc = this;
      alert("Descargando reporte visual");
      html2canvas(vc.showCaptureRef)
        .then(canvas => {
          vc.document.body.appendChild(canvas);
        })
        .catch(error => {
          console.log("Erorr descargando reporte visual");
          alert("Error descargando el reporte visual");
        });
    },*/
    downloadVisualReport() {
      let self = this;
      //console.log(self);
      let filename = "Reporte de asdlsdjlfs.png";
      html2canvas(self.showCaptureRef(), {
        width: 600,
        height: 600
      })
        .then(canvas => {
          //console.log(canvas)
          document.body.appendChild(canvas);
          var a = document.createElement("a");
          a.href = canvas.toDataURL("image/png");
          a.download = "myfile.png";
          a.click();
        })
        .catch(error => {
          //console.log(error);
          alert("Error descargando el reporte visual");
        });
    }
  },
  components: {
    QrcodeVue
  }
};
</script> 