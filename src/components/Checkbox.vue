<template>
  <div class="agree-wrap">
    <label>
      <input
          type="checkbox"
          :value="value"
          :checked="isChecked"
          @change="update"
      >
      <span>{{label}}</span>
    </label>
  </div>
</template>

<script>
export default {
  name: "Checkbox",
  model: {
    event: 'change',
    prop: 'nValue'
  },
  props: {
    value: String,
    trueValue: String,
    falseValue: String,
  label: String,
    nValue: {
      default: ''
    }
  },
  computed: {
    isChecked() {
      if(this.nValue instanceof Array) {
        return this.nValue.includes(this.value)
      }
      return this.nValue === this.value
    }
  },
  methods: {
    update(e) {
      let isCheck = e.target.checked;

      if(this.nValue instanceof Array) {
        let newValue = [...this.nValue];

        if(isCheck) {
          newValue.push(this.value)
        } else {
          newValue.splice(newValue.indexOf(this.value))
        }

        this.$emit('change', newValue)
      } else {
        this.$emit('change', isCheck ? this.trueValue : this.falseValue);
      }
    }
  }
}
</script>

<style scoped>
.agree-wrap{
  width: 100px;
  margin: 10px auto;
}
</style>