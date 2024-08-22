<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- {{ message }} -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Transition/>
    <SlotDemo/>

  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import Transition from './components/TransitionDemo.vue'
import SlotDemo from './components/SlotDemo.vue'

//混入 创造一个更小的vue组件挂载到APP上  组件本身有message 就用本身的 
//同名的钩子函数created  在组件本身的钩子执行之前执行
//4大生命周期的顺序 是 先mixin 的created 再内部的created  然后mounted 再内部的mounted
const mixin = {
  data(){
    return {
      message:"XXX Hello World",
    }
  },
  created(){
    console.log('mixin------------我是mixin里的created 我先执行');
    this.sayHello();
  },
  mounted(){
    console.log('mixin------------我是mixin里的mounted 我先执行');
  },
  methods:{
    sayHello(){
      console.log('hello');
    }
  }
}

export default {
  name: 'App',
  mixins:[mixin],
  components: {
    // HelloWorld,
    // Transition,
    SlotDemo
  },
  created(){
    console.log('我是内部的created Inner created 我后执行');
  },
  mounted(){
    console.log('我是内部的mounted 我后执行');
  },
  data(){
    return {
      message:"Inner hello world",
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
