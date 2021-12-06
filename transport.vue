<template>
  <van-nav-bar
    title="成品转运"
    left-text="返回"
    left-arrow
    right-text="完成"
    @click-left="onClickLeft"
    @click-right="onClickRight"
  />
  <van-cell-group>
    <van-cell title="提货单位" value="进出口公司" />
    <van-cell title="发货员" :value="username" />
  </van-cell-group>
  <van-cell-group inset>
    <van-field
      v-model="carNO"
      readonly
      label="车牌号"
      @click="carShow = true"
    />

    <van-field v-model="vin" label="机号" placeholder="请扫描机号" readonly />
    <!-- <van-field
      v-model="result"
      is-link
      readonly
      label="批次号"
      placeholder="请选择批次号"
      @click="showPicker = true"
    />
    <van-popup v-model:show="showPicker" position="bottom">
      <van-picker
        :columns="columns"
        @confirm="onConfirm"
        @cancel="showPicker = false"
      />
    </van-popup> -->
  </van-cell-group>

  <van-cell-group>
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
    <van-cell title="单元格" value="内容" />
  </van-cell-group>
  <vnp-keyboard
    v-bind:value="carNO"
    v-on:input="carNO = $event"
    v-model:show.sync="carShow"
  />
</template>

<script lang="ts">
import { Dialog } from "vant";
import { defineComponent, ref } from "vue";
import { useRouter } from "vue-router";
import { GetZYScanByParam } from "@/api/transport";
import Keyboard from "@/components/vant-number-plate/vnp-keyboard.vue";
export default defineComponent({
  name: "Transport",
  components: {
    "vnp-keyboard": Keyboard,
  },
  setup() {
    const username = localStorage.getItem("user");
    const carNO = ref("");
    const carShow = ref(false);
    const vinlist = ref([""]);
    const vin = ref("");
    const vinDetailList = ref([{}]);
    const showPicker = ref(false);
    const result = ref([{}]);
    const router = useRouter();
    const carNOField = ref();
    const onClickRight = () => {
      Dialog.confirm({
        title: "提示",
        message: "是否装车完毕？",
      })
        .then(() => {
          router.push({ name: "Home" });
        })
        .catch(() => {
          // on cancel
        });
    };

    const onClickLeft = () => {
      router.go(-1);
    };
    return {
      showPicker,
      username,
      carNO,
      carShow,
      carNOField,
      result,
      vin,
      vinlist,
      vinDetailList,

      onClickRight,
      onClickLeft,
    };
  },
});
</script>

<style lang="less" scoped>
.van-cell-group:nth-last-child(1) {
  overflow-y: scroll;
  height: 250px;
}
</style>
