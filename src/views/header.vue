<template>
  <fixed-header>
    <div class="navbar">
      <img class="rouded-circle" :src="`${publicPath}logo.jpg`" />
    </div>
  </fixed-header>
</template>
 
<script>
import FixedHeader from "vue-fixed-header";

export default {
  components: {
    FixedHeader,
  },
  data() {
    return {
      publicPath: process.env.BASE_URL,
    };
  },
};
</script> 
 
<style>
.navbar.vue-fixed-header--isFixed {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
}
</style> 