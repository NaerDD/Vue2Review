<template>
    <div class="hello">
        <button v-on:click="show = !show">Toggle</button>
        <!-- <transition name="fade"> -->
            <!-- 
             v-if是 条件渲染 从dom节点上删除增加节点 会造成重排重绘 
            v-show是添加css属性  display   展示与隐藏 dom节点上不会删除 只会造成重绘 不会造成重排 对性能影响小


            v-if 是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

            v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

            相比之下， v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

            一般来说， v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件不太可能改变，则使用 v-if 较好。

            -->
            <!-- <p v-if="show">hello</p> -->
            <!-- <p v-show="show">hello</p> -->
        <!-- </transition> -->
        <!-- <h1 class="animate__animated animate__bounce">An animated element</h1> -->
         <!-- 
              v-on:before-enter="beforeEnter"
              enter会替换原本的进入动效
              v-on:enter="Enter"
              v-on:after-enter="afterEnter"
              v-on:enter-cancelled="enterCancelled"
              v-on:before-leave="beforeLeave"
              v-on:leave="leave"
              v-on:after-leave="afterLeave
              v-on:leave-cancelled="leaveCancelled"
         -->
        <transition 
            name="custom-classes-transition"
            
            leave-active-class="animated bounceOutRight"
            v-on:before-enter="beforeEnter"
            v-on:before-leave="beforeLeave"
            >
            <p v-show="show">hello</p>
        </transition>
      
    </div>
  </template>
  
  <script>
  export default {
    data(){
        return {
            show:true,
        }
    },
    methods:{
      //钩子函数本身跟 副作用概念类似
      beforeEnter(el,done){
        console.log('enter');
        document.body.style.background="orange";
        document.body.style.transition="all .5s ease";
        //比如做一些动画执行完毕后的特殊处理  清除元素...

        done();
        done();
      },
      beforeLeave(el,done){
        console.log('leave');
        document.body.style.background="white";
        document.body.style.transition="all .5s ease";
        done();

      }
    }
  }
  </script>
  <style scoped>
  /* .fade-enter-active,.fade-leave-active{
    transition: all .5s;
    transform: translate(0);
  }
  .fade-enter,.fade-leave-to{
    opacity:0;
    transform: translate(-100px);
  } */
  </style>