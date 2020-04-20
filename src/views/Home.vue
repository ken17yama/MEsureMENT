<template>
  <div class="home container">
    <img alt="Vue logo" src="../assets/logo.png" class="logo" />
    <Mesure></Mesure>
  </div>
</template>

<script>
// @ is an alias to /src
import Mesure from "@/components/Mesure.vue";

export default {
  name: "Home",
  components: {
    Mesure
  }
};
</script>
<style scoped>
.logo {
  height: 20vh;
}
</style>
