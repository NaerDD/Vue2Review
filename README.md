# vue-advanced

## Project setup
```
很久没碰前端了 复习一下 将代码放在这里做备份
```
## 1.在vue中 如果有多个组件都需要用到同一个方法如何将这个方法提取出来？
在 Vue 中，如果有多个组件都需要用到同一个方法，可以通过以下几种方式将该方法提取出来，以避免代码重复：

Mixins：使用 Vue 的 mixin 功能。你可以创建一个 mixin，将需要共享的方法放在其中。然后让需要使用这些方法的组件引入这个 mixin。这样，这些组件就可以使用 mixin 中定义的方法了。

// myMixin.js
export const myMixin = {
  methods: {
    myMethod() {
      //...
    }
  }
};

在组件中使用 mixin：
import { myMixin } from './myMixin.js';

export default {
  mixins: [myMixin],
  methods: {
    anotherMethod() {
      this.myMethod(); 
    }
  }
};

2.Vuex：如果你需要共享的方法涉及到状态管理，那么可以考虑使用 Vuex。在 Vuex 中，你可以创建 actions、mutations 和 getters，这些都可以被多个组件共享。

// store.js
const store = new Vuex.Store({
  state: {
    //...
  },
  mutations: {
    myMutation(state) {
      //...
    }
  },
  actions: {
    myAction(context) {
      // context 对象包含 dispatch、commit 和 state 等属性，方便你在 actions 中执行其他方法
      context.commit('myMutation'); 
    }
  },
  getters: {
    myGetter(state) {
      //...
    }
  }
});
在组件中使用 Vuex：
import { mapActions, mapMutations, mapGetters } from 'vuex';

export default {
  computed: {
   ...mapGetters(['myGetter']),
  },
  methods: {
   ...mapActions(['myAction']),
   ...mapMutations(['myMutation']),
    anotherMethod() {
      this.myMethod(); 
    }
  }
};

3.单独的 JavaScript 文件：你也可以创建一个单独的 JavaScript 文件，将公共方法放在里面。然后在需要使用这些方法的组件中引入这个文件。这种方式在功能集中且不需要状态管理的情况下特别有用

// utils.js
export function myMethod() {
  //...
}

在组件中引入并使用，请注意，如果这种方式使用 this 需要绑定一个 vue 实例：
import { myMethod } from './utils.js';

export default {
  data() {
    return { utils: myMethod } 
  },
  methods: {
    anotherMethod() {
      this.utils(); 
    }
  }
};

4.Plugin：在一些复杂的情况下，你可以创建一个 Vue 插件。这允许你封装更多的逻辑，包括但不限于方法、组件、指令等。
// myPlugin.js
MyPlugin.install = function (Vue, options) {
  Vue.prototype.$myMethod = function () {
    //...
  };
};
在入口文件（如 main.js）中安装插件：
import MyPlugin from './myPlugin';

Vue.use(MyPlugin);

在组件中使用：
export default {
  methods: {
    anotherMethod() {
      this.$myMethod(); 
    }
  }
};
综上所述，使用哪种方法取决于你的具体需求和项目结构。如果需要共享的方法比较简单，可以使用 mixins 或单独的 JavaScript 文件。如果涉及到状态管理，Vuex 是个不错的选择。如果需要封装更多的功能或创建可重用组件集合，插件可能是最合适的。