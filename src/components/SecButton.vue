<script setup>
import { ref } from 'vue'
import { ChevronRight } from 'lucide-vue-next'
defineProps({
  btnText: {
    type: String,
    default: 'Button',
    required: true,
  },
  btnAction: {
    type: Function,
    required: false,
  },
  btnLink: {
    type: Function,
    required: false,
  },
})

const iconColor = ref('#00566b')

const changeColor = (isHovering) => {
  iconColor.value = isHovering ? '#00566b' : '#00566b'
}
</script>

<template>
  <button class="button" @mouseenter="changeColor(true)" @mouseleave="changeColor(false)">
    {{ btnText }}
    <ChevronRight :color="iconColor" />
  </button>
</template>

<style scoped>
.button {
  border: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 5px;
  color: #00566b;
  background-color: #fff;
  font-family: 'Open Sans', sans-serif;
  padding: 10px 17px;
  font-size: 14px;
  line-height: 19.8px;
  text-align: center;
  font-weight: 600;
  min-width: fit-content;
  border-radius: 5px;
}

.button:hover {
  color: '#00566B';
  background-color: #ffb500;
}
</style>
