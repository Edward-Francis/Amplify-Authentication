<template>
  <div id="app">
    <v-toolbar>
      <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title>Title</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn to="/" flat>Home</v-btn>
        <v-btn to="/about" flat>About</v-btn>
        <v-btn to="/signUp" flat v-if="getUser">Sign Up</v-btn>
        <v-btn to="/signUpConfirm" flat v-if="getUser">Confirm</v-btn>
        <v-btn to="/signIn" flat v-if="getUser">Sign In</v-btn>
        <v-btn @click="signOut" flat v-if="!getUser">Sign Out</v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <router-view />
  </div>
</template>

<script>
import { signOut } from "@/utils/auth.js";
export default {
  methods: {
    signOut() {
      signOut()
        .then(data => console.log("DONE", data))
        .catch(err => console.log("SIGN OUT ERR", err));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
