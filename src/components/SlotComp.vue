<template>
   <div>
     <div>子组件</div>
     <!-- 这里父级传递的值 会替换掉slot中原本的值 -->
     <!-- <div>插槽位置<slot>我是默认内容</slot></div> -->
     <!-- 有几个slot就会替换几个 -->
     <!-- <div>插槽位置<slot>我是默认内容</slot></div> -->
     <!-- 如何将内容传到指定的class中  具名插槽 
         用 <template v-slot:header>
            <div>我是头部</div>
         </template> 来指定传递
     -->
     <div> <slot name="header" :msg="msg">我是头部</slot></div>
     <div><slot>我是内容</slot></div>
     <div> <slot name="footer" msg-footer="内部的底部数据">我是底部</slot></div>
   </div>
</template>
<script>
export default {
   name: 'SlotComp',
   data(){
    return{
      msg:"内部的数据",
    }
   }
};
</script>
