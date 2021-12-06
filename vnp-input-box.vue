<template>
  <div class="vnp-input-box">
    <ul>
      <li
        v-for="(item, index) in valist"
        :key="index"
        :class="{ active: activeIndex === index }"
        @click="handleClickItem(index)"
      >
        <span>{{ item }}</span>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from "vue";

export default defineComponent({
  props: {
    value: {
      type: String,
      default: "",
    },
    editable: {
      type: Boolean,
      default: false,
    },
  },
  name: "Box",
  setup(props, context) {
    const valist = ref(["", "", "", "", "", "", "", ""]);
    const activeIndex = ref(0);

    const handleClickItem = (index: number) => {
      if (!props.editable) {
        return;
      }
      activeIndex.value = index;
    };

    const setValue = (data: string) => {
      valist.value[activeIndex.value] = data;
      if (activeIndex.value < 7) {
        activeIndex.value += 1;
      }
    };
    const del = () => {
      valist.value[activeIndex.value] = "";
      if (activeIndex.value > 0) {
        activeIndex.value -= 1;
      }
    };
    watch(activeIndex, () => {
      context.emit("activeChange", activeIndex.value);
    });
    watch(
      valist.value,
      () => {
        context.emit("input", valist.value.join(""));
      }
    );
    watch(
      () => props.value,
      () => {
        console.log(props.value);
        if (valist.value.join("") === props.value) {
          return;
        }
        const val = props.value.split("");
        if (props.editable) {
          activeIndex.value = val.length;
        }
        while (val.length < 8) {
          val.push("");
        }

        valist.value = val;
      },
      { immediate: true }
    );
    return {
      valist,
      activeIndex,
      setValue,
      handleClickItem,
      del,
    };
  },
});
</script>

<style lang="less" scoped>
.vnp-input-box {
  padding: 10px 0;
  border: 1px solid #d8d8d8;
  border-radius: 2px;
  color: #8d8d8d;
  font-size: 15px;
  text-align: center;

  ul {
    display: flex;
  }
  li {
    flex: 1;
    border-right: 1px solid #eaeaea;
    height: 28px;
    line-height: 28px;

    &:first-child {
      border-color: #a6a6a6;
      flex: 1.3;
    }
    &:last-child {
      border: none;
    }
    &.active {
      color: #1989fa;

      > span {
        height: 100%;
        width: 20px;
        display: inline-block;
        border-bottom: 1px solid #1989fa;
      }
    }
  }
}
</style>
