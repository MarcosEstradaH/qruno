<template>
  <div id="app">
    <generadors/>
  </div>
</template>

<script>
import Generador from "./views/Generador.vue";
import Generadors from "./views/Generadors.vue";

export default {
  name: "App",
  components: {
    Generador,
    Generadors
  }
};
</script>
