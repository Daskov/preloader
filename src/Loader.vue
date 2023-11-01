<template>
  <div v-if="isLoading" class="loader"/>
</template>

<script setup>
defineProps({
  isLoading: {
    type: Boolean,
    required: true,
  },
});
</script>

<style scoped>
.loader {
  border-top: 4px solid blue;
  border-right: 4px solid blue;
  border-bottom: 4px solid blue;
  border-left: 4px solid #fff;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  animation: spin 1.5s linear infinite;
  margin: auto;
  clip: rect(0px, 25px, 50px, 0px);
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
