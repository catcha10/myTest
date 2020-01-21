<template>
  <div class="app" >
    <Header />
    <TheSideNav/>
    <div class="app-content" :class="[toggleSidebar==true ? 'open' : 'close']" >
        <nuxt />
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from "~/components/Header.vue";
import Footer from "~/components/Footer.vue";
import TheSideNav from '~/components/sideNav.vue';
export default {
  components: {
    Header,
    Footer,
    TheSideNav
  },
  computed: {
      toggleSidebar() {
          return this.$store.getters['nav/toggleSidebar']
      }
  }
};
</script>

<style>
    html, body{
      margin: 0;
      height: 100%;
      width: 100%;
      font-size:16px;
    }
    .app{
      max-width:100%;
      overflow:hidden;
    }
    .app-container{
      height: 100%;
      position: relative;
    }
    .app-content{
      min-height: 100vh;
      padding: 24px;
      transition: all 0.3s ease-out;
    }
    .app-content.open{
      transform: translateX(300px);
    }
    .app-content h1{
      font-size:1.5rem;
      font-family: helvetica;
      font-style: normal;
      font-weight: 300;
      color:#333;
    }
</style>