<template>
  <div class="radio-wrap">
    <label>
      <input
          type="radio"
          :value="value"
          :checked="isChecked"
          @change="$emit('change', $event.target.value)"
      >
      <span>{{label}}</span>
    </label>
  </div>
</template>

<script>
export default {
 name: "Radio",
  model: {
    event: 'change',
    prop: 'nValue'
  },
  props: {
    value: String,
    label: String,
    nValue: {
      default: ''
    },

  },
  computed: {
    isChecked() {
      return this.nValue === this.value
    }
  }
}
</script>

<style scoped>
  .radio-wrap{
    width: 100px;
    text-align: left;
    margin: auto;
  }
</style>