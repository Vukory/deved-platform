<template>
  <a v-show="showButton" href="#" class="Back-to-top Vlt-btn Vlt-btn--primary Vlt-btn--icon" @click.prevent="toTop">
    <svg class="Vlt-icon Vlt-icon--large Vlt-white">
      <use xlink:href="../node_modules/@vonagevolta/volta2/dist/symbol/volta-icons.svg#Vlt-icon-arrow-thin-up" />
    </svg>
  </a>
</template>

<script>
export default {
  data() {
    return {
      showButton: false
    }
  },

  created () {
    if (!this.$isServer) {
      window.addEventListener('scroll', this.handleScroll)
    }
  },

  destroyed () {
    if (!this.$isServer) {
      window.removeEventListener('scroll', this.handleScroll)
    }
  },

  methods: {
    toTop () {
      if (!this.$isServer) {
        const increments = (0 - window.pageYOffset)/(500/16)
        // Loop the animation function
        const runAnimation = setInterval(() => {
            window.scrollBy(0, increments)
            if (window.pageYOffset <= document.body.offsetTop) {
                clearInterval(runAnimation)
            }
        }, 16)
      }
    },
    handleScroll () {
      if (!this.$isServer) {
        if (window.pageYOffset > 200) {
          this.showButton = true
        } else {
          this.showButton = false
        }
      }
    }
  }
}
</script>

<style scoped>
  .Back-to-top {
    z-index: 1;
    position: fixed;
    bottom: 50px;
    right: 5%;
  }
</style>