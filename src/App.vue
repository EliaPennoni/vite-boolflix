<script>
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppFooter from "./components/AppFooter.vue";
export default {
  data() {
    return {
  
    };
  },
  created() {
    axios
      
  },
  computed: {
    
  },
  components: {
    AppHeader,
    AppMain,
    AppFooter
  },
};

</script>

<template>
    <AppHeader />

    <AppMain />

    <AppFooter />
</template>

<style lang="scss" scoped>
    @import "bootstrap/scss/bootstrap";
</style>
