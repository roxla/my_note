## vue3 webpack5 下的 qiankun 配置

### main

#### APP.vue

```vue
<template>
  <router-link to="/vue">About</router-link>
  <div id="container"></div>
</template>
```

#### main.js

```js
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";

import { registerMicroApps, start, setDefaultMountApp } from "qiankun";

// 在主应用中注册子应用
registerMicroApps([
    {
        name: "vue app",
        entry: "http://localhost:7105/", // 重点8：对应重点6
        container: "#container", // 重点9：对应重点2
        activeRule: "/vue", // 重点10：对应重点4
        props: {
            appContent: "我是子应用传给主应用的值",
        },
    },
]);
setDefaultMountApp("/vue");
// 启动
start();

createApp(App).use(store).use(router).mount("#app");
```

#### vue.config.js

```js
const { defineConfig } = require("@vue/cli-service");
module.exports = defineConfig({
    transpileDependencies: true,
    devServer: {
        headers: {
            // 重点1: 允许跨域访问子应用页面
            "Access-Control-Allow-Origin": "*",
        },
    },
});
```

### service

#### router.js

```js
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]

const router = createRouter({
  // 判断是否作为微应用加载
  history: createWebHistory(window.__POWERED_BY_QIANKUN__ ? "/vue" : "/"),
  routes
})

export default router

```

#### main.js

```js
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";

let instance = null;

if (window.__POWERED_BY_QIANKUN__) {
    // eslint-disable-next-line no-undef
    __webpack_public_path__ = window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__;
}

function render(props = {}) {
    const { container } = props;

    instance = createApp(App);
    instance.use(router);
    instance.mount(container ? container.querySelector("#app") : "#app");
}

if (!window.__POWERED_BY_QIANKUN__) {
    render();
}

export async function bootstrap() {
    console.log("%c ", "color: green;", "vue3.0 app bootstraped");
}

export async function mount(props) {
    console.log('[vue] props from main framework', props);
    render(props);
    instance.config.globalProperties.$onGlobalStateChange =
        props.onGlobalStateChange;
    instance.config.globalProperties.$setGlobalState = props.setGlobalState;
}

export async function unmount() {
    instance.unmount();
    instance._container.innerHTML = "";
    instance = null;
}

```

#### vue.config.js

```js
const path = require('path');
const { name } = require('./package');

function resolve(dir) {
  return path.join(__dirname, dir);
}

const port = 7105;

module.exports = {
  outputDir: 'dist',
  assetsDir: 'static',
  filenameHashing: true,
  devServer: {
    port,
    headers: {
      'Access-Control-Allow-Origin': '*',
    },
  },
  // 自定义webpack配置
  configureWebpack: {
    resolve: {
      alias: {
        '@': resolve('src'),
      },
    },
    output: {
      // 把子应用打包成 umd 库格式
      library: {
        name: `${name}-[name]`,
        type: 'umd',
      }
    },
  },
};
```

