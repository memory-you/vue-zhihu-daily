<template>
  <div id="app">
    <keep-alive :exclude="['detail','comment','collect']">
      <router-view />
    </keep-alive>
  </div>
</template>

<script>
export default {
  name: 'app',
  // 解决页面刷新vuex数据丢失的问题
  created() {
    // 在页面加载时读取sessionStorage里的状态信息
    if (sessionStorage.getItem('store')) {
      this.$store.replaceState(
        Object.assign(
          {},
          this.$store.state,
          JSON.parse(sessionStorage.getItem('store')),
        ),
      );
    }

    // 在页面刷新时将vuex里的信息保存到sessionStorage里
    window.addEventListener('beforeunload', () => {
      sessionStorage.setItem('store', JSON.stringify(this.$store.state));
    });
  },
};
</script>

<style lang="less">
#app {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: @bgColor;
}
</style>
