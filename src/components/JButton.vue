<template>
  <button class="j-btn">
    <slot name="icon" v-if="preIcon">
      <j-icon :icon="preIcon" size="default" />
    </slot>
    <slot>Click Me</slot>
    <slot name="appendIcon" v-if="appendIcon">
      <j-icon :icon="appendIcon" size="default" />
    </slot>
  </button>
</template>

<script setup>
import JIcon from "@/components/JIcon.vue";
import {computed} from "vue";

const props = defineProps({
  preIcon: {
    type: String
  },
  color: {
    type: String,
    default: '#2c3e50'
  },
  appendIcon: {
    type: String
  }
})

/**
 * 根據背景色決定文字的顏色
 * @type {ComputedRef<string>}
 */
const textColor = computed(() => {
  const rgb = props.color.replace(/^#?([a-f\d])([a-f\d])([a-f\d])$/i
      , (m, r, g, b) => '#' + r + r + g + g + b + b)
      .substring(1).match(/.{2}/g)
      .map(x => parseInt(x, 16))

  return (rgb[0] * 0.299 + rgb[1] * 0.587 + rgb[2] * 0.114) > 186
      ? '#333333' // 黑色文字
      : '#ffffff' // 白色文字
})

</script>

<style lang="scss" scoped>
.j-btn {
  padding: 5px 10px;
  margin: 2px 4px;
  border-radius: 8px;
  color: v-bind(textColor);
  border: 1px solid v-bind(textColor);
  cursor: pointer;
  font-family: "Noto Sans TC", sans-serif;
  background-color: v-bind(color);

  display: flex;
  align-items: center;
  gap: 4px;

  &:hover {
    outline: 2px solid v-bind(color);
    filter: brightness(1.5);
  }

  &:active {
    filter: brightness(1);
  }
}
</style>