# learn-vue

## vue-cli 설치

```shell
$ npm install -g @vue/cli
```



## Project 생성

```shell
$ vue create test
```

default로 설치



## Project 기본 구조

```markdown
- /node_modules
- /public
  - /index.html
- /src
  - /assets
  - /components
  - /views
  - /App.vue
  - /main.js
- /.gitignore
- /babel.config.js
- /package-lock.json
- /package.json
- README.md
```

- /public

  번들링된 파일

- /src/assets

  정적 파일이 보관되는 곳

- /src/components

  컴펀넌트

- /src/App.vue

  컴펀넌트가 

- /src/main.js

  Vue 컴펀넌트가 렌더링 되는 곳 / Vue 설정

- /src/views

  페이지

- /babel.config.js

  babel 설정

- /package.json



## 의존성 모듈 설치

```shell
$ npm install --save vue-router bootstrap bootstrap-vue
```

- vue-router

  vue에서 라우팅 기능을 사용하여 SPA(Single Page Application) 구성하기 위한 의존성 모듈.

- bootsrap, bootstrap-vue

  vue을 학습하면서 스타일에 신경쓰지 않고, vue 핵심 개념에 더 집중하기 위해 사용.

  vue에서 bootstrap을 사용하기 위해서는 bootstrap-vue도 설치를 해야 함.



## vue 파일 기본  구조

```vue
<template>
	...
</template>

<script>
	...
</script>
```

- <code><template></template></code>

  사용자 UI를 작성하는 영역으로 html 코드가 작성되는 곳.

- <code><script></script></code>

  스크립트 작성을 위한 영역.



## Bootstrap 설정

/src/main.js

```javascript
import Vue from 'vue'
import App from './App.vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

// Import Bootstrap an BootstrapVue CSS files (order is important)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

// Make BootstrapVue available throughout your project
Vue.use(BootstrapVue)
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin)

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
}).$mount('#app')
```

vue 루트 파일

- <code>import Vue from 'Vue'</code>

  vue 의존성 불러온다.

- <code>import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'</code>

  bootsrap 의존성 불러온다.

- <code>import 'bootstrap/dist/css/bootstrap.css'</code>

  <code>import 'bootstrap-vue/dist/bootstrap-vue.css'</code>

  bootstrap 스타일 파일을 불러온다.

- <code>Vue.use()</code>

  Vue에서 Plugin(의존성 모듈)을 사용하기 위해 사용한다.

  반드시 <code>new Vue()</code>전에 사용해야 된다.

- <code>new Vue({ ... }).$mount('#app')</code>

  코드가 이해가 되지 않아 찾아 보았다. 찾아 보니, 아래 코드를 간랸하게 사용하는 것이라고 한다.

  ```
  new Vue({ render: createElement => createElement(App) ).$mount('#app')
  ```



## vue-router 설정 및 레이아웃 구성

/src/components/layout/Header.vue

```vue
<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">NavBar</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
          <b-nav-item href="#" disabled>Disabled</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
  export default {
    name: "header"
  }
</script>
```

- <code><template>...</template></code>

  bootstra에서 제공하는 컴포넌트를 이용하여 header 컴포넌트를 만들었다.

- <code><script>export default { ... }</script></code>

  <code>name</code>은 컴포넌트 이름을 지정할 때 사용한다. 필수적으로 사용하지 않았도 된다.



/src/views/Home.vue

```vue
<template>
  <div>
    <h1>Welcome to Home!</h1>
  </div>
</template>

<script>
  export default {
    name: "home"
  }
</script>
```

vue-router 기본 구성을 위한 페이지



/src/views/About.vue

```vue
<template>
  <div>
    <h1>About Page</h1>
  </div>
</template>

<script>
  export default {
    name: "about"
  }
</script>
```

vue-router 기본 구성을 위한 페이지



/src/router.js

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'

import Home from './views/Home'
import About from './views/About' 

Vue.use(VueRouter)

const router = new VueRouter({
  mode: "history",
  routes: [
    { path: "/", component: Home },
    { path: "/about", component: About }
  ]
});

export default router
```

vue-router 설정 파일

- <code>import VueRouter form 'vue-router'</code>

  vue-router 의존성 모듈을 불러왔다.

- <code>Vue.use(VueRouter)</code>

  vue에서 vueRouter을 사용한다는 의미.

- <code>const router = new VueRouter({ ... })</code>

  <code>VueRouter</code> 생성.

- <code>mode</code>

  vue-router 기본 모드는 hash 모드이다. 그렇기 때문에 HTML5 HISTORY API 기반으로 동작하기 위해 코드 상에 명시해주었다.

- <code>routes</code>

  URI에 따라 컴펀넌트 매핑을 하는 부분이다.

- <code>export default router</code>

  정의한 router 객체를 반환.



/src/main.js

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

// Import Bootstrap an BootstrapVue CSS files (order is important)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

// Make BootstrapVue available throughout your project
Vue.use(BootstrapVue)
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin)

Vue.config.productionTip = false

new Vue({
  router, 
  render: h => h(App),
}).$mount('#app')
```

- <code>import router from './router'</code>

  위에서 생성한 router을 불러온다.

- <code>new Vue({ router, render: h => h(App) }).$mount('#app')</code>

  Vue 객체를 생성할 때, router을 같이 전달한다.



/src/App.vue

```vue
<template>
  <div id="app">
    <Header />
    <div id="content" class="content">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue'

export default {
  name: 'App',
  components: {
    Header
  }
}
</script>
```

레이아웃 구성

- <code><router-view></router-view></code>

  URI에 따라 동적으로 변경되는 부분이다.

- <code>impot Header from './components/layout/Header.vue'</code>

  위에서 정의한 header 컴펀넌틀 불러온다.

- <code>export default { ... components: { Header } ... }</code>

  <code><template></code>에 Header 컴포넌트를 전달을 한다.



## 데이터 바인딩 및 Form 제어

/src/views/Home.vue

```vue
<template>
  <div>
    <h1>Welcome to {{title2}}!</h1>
    <input type="text" v-model="input1" />
    <button type="button" @click="getData">Get</button>
    <button type="button" @click="setData">Set</button>

    <select class="form-control" v-model="region" @change="changeRegion">
      <option :key="index" :value="data.v" v-for="(data, index) in options">{{data.t}}</option>
    </select>

    <table class="table table-bordered" v-if="tableShow">
      <tr :key="index" v-for="(data, index) in options">
        <td>{{data.v}}</td>
        <td>{{data.t}}</td>
      </tr>
    </table>

    <table class="table table-bordered" v-show="tableShow">
      <tr :key="index" v-for="(data, index) in options">
        <td>{{data.v}}</td>
        <td>{{data.t}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
  export default {
    name: "home",
    data() {
      return {
        title: "selectjun",
        title2: "Seoul",
        input1: "abcd",
        options: [
          { v: "S", t: "Seoutl" },
          { v: "J", t: "Jenu" },
          { v: "B", t: "Busan" }
        ],
        region: "J",
        tableShow: true
      }
    },
    watch: {
      input1() {
        console.log(this.input1);
      }
    },
    methods: {
      getData() {
        alert(this.input1)
      },
      setData() {
        this.input1 =  "123"
      },
      changeRegion() {
        alert(this.region)
      }
    }
  }
</script>
```

- <code>data()</code>

  사용할 데이터를 정의한다.

- <code>watch</code>

  데이터 변경을 감지 후, 원하는 로직 작성이 가능하다.

  함수 선언 시, 데이터 이름과 동일하게 사용해야 한다.

- <code>methods</code>

  함수들 정의하는 곳이다.

  데이터 접근 시, <code>this</code> 키워드를 사용하여 접근해야 한다.

- <code>v-model</code>

  INPUT value 요소에 데이터 바인딩을 할 때 사용한다.

- <code>v-for</code>

  태그에서 반복문을 사용하고 싶을 때 사용한다.

- <code>v-if</code>

  조건부 렌더링을 할 때 사용한다.

  값이 <code>false</code>인 경우, 렌더링하지 않는다.

- <code>v-show</code>

  렌더링을 하지만 사용자에게 컴펀넌트를 보여주고 싶지 않을 때 사용한다.

  값이 <code>false</code>인 경우, 숨긴다.

- <code>@click</code>, <code>@change</code>

  vue에서 Evnet을 걸 때 사용한다. 값으로 함수가 전달된다.

- {{...}}

  화면에 데이터를 바인딩할 떄 사용한다.



## LifeCycle

/src/views/Home.vue

```vue
<template>
  <div>
    <h1>Welcome to {{title2}}!</h1>
    <input type="text" v-model="input1" />
    <button type="button" @click="getData">Get</button>
    <button type="button" @click="setData">Set</button>

    <select class="form-control" v-model="region" @change="changeRegion">
      <option :key="index" :value="data.v" v-for="(data, index) in options">{{data.t}}</option>
    </select>

    <table class="table table-bordered" v-if="tableShow">
      <tr :key="index" v-for="(data, index) in options">
        <td>{{data.v}}</td>
        <td>{{data.t}}</td>
      </tr>
    </table>

    <table class="table table-bordered" v-show="tableShow">
      <tr :key="index" v-for="(data, index) in options">
        <td>{{data.v}}</td>
        <td>{{data.t}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
  export default {
    name: "home",
    data() {
      return {
        title: "selectjun",
        title2: "Seoul",
        input1: "abcd",
        options: [
          { v: "S", t: "Seoutl" },
          { v: "J", t: "Jenu" },
          { v: "B", t: "Busan" }
        ],
        region: "J",
        tableShow: true
      }
    },
    watch: {
      input1() {
        console.log(this.input1);
      }
    },
    methods: {
      getData() {
        alert(this.input1)
      },
      setData() {
        this.input1 =  "123"
      },
      changeRegion() {
        alert(this.region)
      }
    },
    beforeCreate() {
      console.log("beforeCreate")
    },
    created() {
      console.log("created")
    },
    beforeMount() {
      console.log("beforeMount")
    },
    mounted() {
      console.log("mounted")
    },
    beforeUpdate() {
      console.log("beforeUpdate")
    },
    updated() {
      console.log("updated")
    },
    beforeDestory() {
      console.log("beforeDestory")
    },
    destoryed() {
      console.log("destory")
    }
  }
</script>
```

- <code>beforeCreate()</code>

  페이지가 생성되기 전

- <code>created()</code>

  페이지가 생성이 된 후

- <code>beforeMount()</code>

  DOM에 마운트 되기 전

- <code>mounted()</code>

  DOM에 마운트 된 후

- <code>beforeUpdate()</code>

  업데이트 되기 전

- <code>updated()</code>

  업데이트 된 후

- <code>beforeDestroy()</code>

  페이지 사라지기 전

- <code>destroyed()</code>

  페이지가 사라진 후



## 참고문헌

> **[개발자의 품격] 유튜브에서 제공하는 [한 시간만의 끝내는 Vue.js 입문]** 
>
> ​	https://youtu.be/sqH0u8wN4Rs
>
> **Vue Docs**
>
> ​	https://vuejs.org/
>
> **[Vue] render:h => h(App)**
>
> ​	https://goodteacher.tistory.com/85?category=774667
>
> **HTML5 히스토리 모드**
>
> ​	https://router.vuejs.org/kr/guide/essentials/history-mode.html#%E1%84%89%E1%85%A5%E1%84%87%E1%85%A5-%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC-%E1%84%8B%E1%85%A8%E1%84%8C%E1%85%A6

