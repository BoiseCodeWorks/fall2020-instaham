<template>
  <div id="app">
    <navbar />
    <router-view />
  </div>
</template>

<script>
import Navbar from "@/components/navbar";
import { onAuth } from "@bcwdev/auth0-vue";
import { setBearer, api } from "./services/AxiosService";
export default {
  name: "App",
  async beforeCreate() {
    await onAuth();
    if (this.$auth.isAuthenticated) {
      setBearer(this.$auth.bearer);
      this.$store.dispatch("getProfile");
    }
  },
  components: {
    Navbar,
  },
};
</script>
<style lang="scss">
@import "./assets/_variables.scss";
@import "bootstrap";
@import "./assets/_overrides.scss";
</style>
