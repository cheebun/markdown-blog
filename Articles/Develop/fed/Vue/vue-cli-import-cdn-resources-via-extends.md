在根目录建立 `vue.config.js`

在 `vue.config.js` 中加入

```javascript
module.exports = {
  configureWebpack: {
    externals: {
      vue: "Vue",
      vuex: "Vuex",
      "vue-router": "VueRouter"
    },
  },
}
```
