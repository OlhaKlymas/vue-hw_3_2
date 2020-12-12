<template>
  <form @submit.prevent="$emit('onSubmit')">
    <slot name="title"></slot>
    <slot name="fields"></slot>
    <slot name="select"></slot>
    <slot name="radio"></slot>
    <slot name="checkbox"></slot>
    <slot name="submitBtn"></slot>
  </form>
</template>

<script>
export default {
name: "Wrapper"
}
</script>

<style scoped>

</style>