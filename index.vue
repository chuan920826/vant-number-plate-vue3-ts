<template>
 
  <van-cell-group inset>
    <van-field
      v-model="carNO"
      readonly
      label="车牌号"
      @click="carShow = true"
    />

  </van-cell-group>
  <vnp-keyboard
    v-bind:value="carNO"
    v-on:input="carNO = $event"
    v-model:show.sync="carShow"
  />
</template>

<script lang="ts">

import { defineComponent, ref } from "vue";


import Keyboard from "@/components/vant-number-plate/vnp-keyboard.vue";
export default defineComponent({
  name: "index",
  components: {
    "vnp-keyboard": Keyboard,
  },
  setup() {
   
    const carNO = ref("");
    const carShow = ref(false);
  
    

   
    return {
     
      carNO,
      carShow,
      
    };
  },
});
</script>

