<script setup>
const props = defineProps({
  value:{
    type: String,
    required: true,
  }
})

</script>

<template>
  <button class="btn">
    {{props.value}}
  </button>
</template>

<style scoped lang="scss">

</style>