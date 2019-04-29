<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  methods: {
    detectWebView() {
      if (window.navigator.userAgent) {
        if (/(FBAV|Line|wv|IAB|WebView)/.test(window.navigator.userAgent)) {
          if (/(Android|android)/.test(window.navigator.userAgent)) {
            window.location.href =
              'googlechrome://navigate?url=www.calicomoo.ml/wedding';
          } else if (/(iPod|iPad|iPhone)/.test(window.navigator.userAgent)) {
            window.location.href = 'googlechrome://www.calicomoo.ml/wedding';
          }
        }
      }
    }
  },
  created() {
    this.detectWebView();
  }
};
</script>


<style lang="scss">
html,
body {
  margin: 0;
  padding: 0;
  background-color: #d08490;
  font-family: Helvetica, Arial, Sans-Serif, Microsoft JhengHei;
}
#app {
  text-align: center;
}
</style>
