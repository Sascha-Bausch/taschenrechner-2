<template>
  <div class="home">
    <img alt="SB logo" src="../assets/logo_sb.jpg" />
    <Taschenrechner />
    <!-- msg="Willkommen in der wunderbaren Welt der Mathematik" -->
  </div>
</template>

<script>
// @ is an alias to /src
import Taschenrechner from "@/components/Taschenrechner.vue";

export default {
  name: "Home",
  components: {
    Taschenrechner,
  },
};
</script>

<style scoped>
div {
  font-family: monospace;
}
</style>
