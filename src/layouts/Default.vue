<template>
  <div>
    <div :class="$style.fullPage" v-show="!loaded">
      <table :class="$style.loadingDiv">
        <tr :class="$style.loadingDiv">
          <td>
            <LoadingLogo />
          </td>
        </tr>
      </table>
    </div>
    <v-app v-show="loaded">
      <NavBar :scrolled="scrollfun" />
      <slot />
      <Footer />
    </v-app>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import LoadingLogo from "../components/LoadingLogo";
import NavBar from "../components/NavBar";
import Footer from "../components/Footer";

export default {
  name: "App",
  components: {
    NavBar,
    Footer,
    LoadingLogo
  },
  data() {
    return {
      haveScrolled: false,
      loaded: false
    };
  },
  mounted: function() {
    this.loaded = true;

    document.addEventListener(
      "scroll",
      function() {
        if (window.scrollY >= 50) {
          this.haveScrolled = true;
        } else {
          this.haveScrolled = false;
        }
      }.bind(this)
    );
  },
  computed: {
    scrollfun() {
      if (this.haveScrolled === true) {
        return true;
      } else {
        return false;
      }
    }
  }
};
</script>

<style module lang="css">
.fullPage {
  height:100vh;
  width:100vw;
  text-align:center;
}

.loadingDiv {
  height:100%;
  width:100%;
}
</style>
