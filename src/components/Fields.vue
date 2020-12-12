<template>
  <div class="field">
    <label>
      <span>{{ label }}</span>
      <input :type="type" :value="value" @input="$emit('update:value', $event.target.value)">
    </label>
  </div>
</template>

<script>
export default {
  name: "Fields",
  props: {
    label: String,
    value: String,
    type: {
      type: String,
      default: 'text'
    }
  }
}
</script>

<style scoped>
  .field{
    margin: 10px 0;
  }
  .field label{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 250px;
    margin: auto;
  }
</style>