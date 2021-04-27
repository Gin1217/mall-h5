<template>
  <div id="app">
    <div id="nav">
       <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
    <transition :name="transitionName">
      <router-view class="router-view" />
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      transitionName: "slide-left",
    };
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
@import "./common/style/mixin";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  // height: 100vh;
}
#nav {
  padding: 30px;
  position: absolute;
  top: 0;
  left: 50%;
  z-index: 1000;
}
  a {
    font-weight: bold;
    color: #2c3e50;
.router-view {
  width: 100%;
  height: auto;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: 0 auto;
  -webkit-overflow-scrolling: touch;
}
    &.router-link-exact-active {
      color: #42b983;
    }
  }
.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  height: 100%;
  will-change: transform;
  transition: all 500ms;
  position: absolute;
  backface-visibility: hidden;
}
.slide-right-enter {
  opacity: 0;
  transform: translate3d(-100%, 0, 0);
}
.slide-right-leave-active {
  opacity: 0;
  transform: translate3d(100%, 0, 0);
}
.slide-left-enter {
  opacity: 0;
  transform: translate3d(100%, 0, 0);
}
.slide-left-leave-active {
  opacity: 0;
  transform: translate3d(-100%, 0, 0);
}
</style>