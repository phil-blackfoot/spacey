<template>
  <v-app>
    <AppBar />

    <v-main>
      <router-view />
    </v-main>

    <Footer />
  </v-app>
</template>

<script>
import AppBar from "@/components/AppBar.vue";
import Footer from "@/components/Footer.vue";
export default {
  name: "App",

  data: () => ({}),
  components: { AppBar, Footer },
};
</script>

<style lang="scss">
#app {
  font-family: "Barlow", sans-serif;

  h1 {
    font-size: 36px;
    font-weight: 500;
  }
  h2 {
    font-weight: 600;
  }
  a {
    text-decoration: none;
  }
  .placeholder-picture {
    width: 80px;
  }
}

// scroll styling
body {
  &::-webkit-scrollbar {
    width: 16px;
  }
  &::-webkit-scrollbar-track {
    background-color: #313131;
  }
  &::-webkit-scrollbar-thumb {
    background-color: #90a4ae;
    border-radius: 4px;
    border: 2px solid transparent;
    background-clip: content-box;

    &:hover {
      background-color: #546e7a;
    }
  }
}

// vue fade transitions
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-active {
  transition: opacity 0.4s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
