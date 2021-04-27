<template>
  <div id="app">
    <transition :name="transitionName">
      <router-view class="router-view" />
    </transition>
    <nav-bar></nav-bar>
  </div>
</template>

<script>
import navBar from './components/NavBar.vue';
export default {
  data() {
    return {
      transitionName: "slide-left",
    };
  },
  components: {
    navbar,
  },
  watch: {
    $route(to, from) {
      // 主级到次级
      console.log(this.ShowMenuList);
      if (this.ShowMenuList.includes(to.path)) {
        this.isShowNav = true;
      } else {
        this.isShowNav = false;
      }
      if (to.meta.index > from.meta.index) {
        this.transitionName = "slide-left"; // 向左滑动
      } else if (to.meta.index < from.meta.index) {
        // 由次级到主级
        this.transitionName = "slide-right";
      } else {
        this.transitionName = ""; //同级无过渡效果
      }
    },
  },
};
</script>

<style lang="less">
</style>