# vuex使用

```javascript
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {   //一些操作
    increment (state) {
      state.count++
    }
  },
  getters: {   //getters是对数据封装的一些方法
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
store.commit('increment')  //执行操作
store.commit({
  type: 'increment',   //操作
  amount: 10   //参数
})


```

```
const app = new Vue({
  el: '#app',
  // 把 store 对象提供给 “store” 选项，这可以把 store 的实例注入所有的子组件
  store,   //将store注入各个组件
  components: { Counter },
  template: `
    <div class="app">
      <counter></counter>
    </div>
  `
})
```

```
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({    //子组件引入store中的值
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}

computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])



computed: {
  localComputed () { /* ... */ },
  // 使用对象展开运算符将此对象混入到外部对象中
  ...mapState({
    // ...
  })
}
```

mutation不能包含异步操作，actions可以包含