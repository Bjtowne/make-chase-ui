<template>
  <div id="buttonDiv" />
</template>

<script>
import {appConf} from "@/appConf";

export default {
  name: "GoogleLogin",
  mounted() {
    // eslint-disable-next-line
    google.accounts.id.initialize({
      client_id: appConf.google.clientId,
      callback: this.login
    });
    // eslint-disable-next-line
    google.accounts.id.renderButton(
      document.getElementById("buttonDiv"),
      { theme: "outline", size: "large" }  // customization attributes
    );
  },
  methods:{
    async login(jwt){
      document.cookie = "g_state=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
      let result = await this.$store.dispatch('login',jwt)
      this.$emit('login',result);
    }
  }
}
</script>

<style scoped>

</style>