<template>
   <div class="hello" @click="transform">
    父组件
     <SlotComp>
        <!-- <div>我是slotDemo 父级传进来的</div> -->

         <template v-slot:header="header">
            <div>我是头部{{ message }}---{{ header.msg }}</div>
         </template>
         <!-- 默认slot是<slot v-slot:default> </slot> -->
         <template>
            <div>我是身体{{ message }}</div>
         </template>
         <template v-slot:footer="footer">
            我是底部{{ message }}---{{  footer.msgFooter }}
         </template>
     </SlotComp>
   </div>
</template>
<script>
import SlotComp from './SlotComp.vue';

export default {
   

   data() {
     return {
       message:'SlotDemo'
     }
   },
   components: {
      SlotComp
   },
   methods: {
    transform(){
      //在这个地方拿到vue实例  
      console.log(this.$root);
        this.message = this.message === this.message.toUpperCase()? this.message.toLowerCase() : this.message.toUpperCase();
    }
   }
};
</script>