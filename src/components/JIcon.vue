<template>
  <i :class="getIconClass"></i>
</template>

<script setup>
import {computed} from "vue";

const props = defineProps({
  icon: {
    type: String,
    required: true
  },
  size: {
    type: String,
    default: 'default',
    validator: value => ['small','medium','default','large','extra-large'].indexOf(value) !== -1
  }
});

const getIconClass = computed(() => {
  const sizeMapping = {
    'small': 'mdi-12px',
    'default': 'mdi-16px',
    'medium': 'mdi-24px',
    'large': 'mdi-28px',
    'extra-large': 'mdi-40px'
  };

  const sizeClass = sizeMapping[props.size];

  return {
    'mdi': true,
    [props.icon]: true,
    [sizeClass]: true
  };
});
</script>

<style scoped>
.mdi-12px{
  font-size: 12px;
}

.mdi-16px{
  font-size: 16px;
}

.mdi-24px{
  font-size: 24px;
}

.mdi-28px{
  font-size: 28px;
}

.mdi-40px{
  font-size: 40px;
}
</style>
