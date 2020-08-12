<template>
  <div class="toast" v-if="isShow" @showToast="showHandler()">
    {{ text }}
  </div>
</template>

<script>
export default {
  props: ["text"],
  data() {
    return {
      isShow: false
    };
  },
  methods: {
    showHandler() {
      this.isShow = true;
      setTimeout(() => {
        this.isShow = false;
      }, 2000);
    }
  }
};
</script>

<style lang="sass" scoped>
.toast
  position: fixed
  top: 20px
  right: 20px
  background-color: orangered
  color: #ffffff
  padding: 10px 20px
  text-transform: uppercase
</style>
