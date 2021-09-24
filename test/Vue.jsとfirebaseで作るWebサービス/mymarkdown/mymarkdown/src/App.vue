<template>
  <div id="app">
    <Home v-if="!isLogin" />
    <Editor v-if="isLogin" :user="userData" />
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Editor from "./components/Editor.vue";
export default {
  name: "app",
  data() {
    return {
      isLogin: false,
      userData: null,
    };
  },
  created: function () {
    firebase.auth().OnAuthStateChanged((user) => {
      console.log(user);
      if (user) {
        this.isLogin = ture;
        this.userData = user;
      } else {
        this.isLogin = false;
        this.userData = null;
      }
    });
  },
  components: {
    Home: Home,
    Editor: Editor,
  },
};
</script>