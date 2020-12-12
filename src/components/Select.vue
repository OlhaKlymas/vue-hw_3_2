<template>
  <div class="select-wrap">
    <div class="select"
         @click="showOptions = !showOptions, isSelected = !isSelected"
         :class="{'active': isSelected}">
      {{value ? value : 'Choose language'}}
      <span></span>
    </div>
    <div class="option"
         v-show="showOptions"
         v-for="(val, key) in lang"
         :key="key"
         :label="val"
         @click="selected(val)"
    >{{ val }}</div>
  </div>
</template>

<script>
export default {
  name: 'Select',
  props: {
    lang: {
      type: Array
    },
    select: {
      default: false
    },
    value: {
      default: false
    }
  },
  data(){
    return {
      showOptions: false,
      isSelected: false
    }
  },
  methods: {
    selected(newVal) {
      this.showOptions = !this.showOptions
      this.isSelected = !this.isSelected
      this.$emit('update:value', newVal )
    }
  }
}
</script>

<style scoped>
  .select-wrap{
    width: 300px;
    text-align: center;
    margin: 20px auto;
  }
  .option, .select{
    padding: 10px 20px;
    cursor: pointer;
  }
  .select{
    position: relative;
    border: 1px solid #ccc;
    background: #fff;
  }
  .select.active span{
    transform: rotate(45deg);
  }
  span{
    position: absolute;
    right: 10%;
    display: inline-block;
    width: 10px;
    height: 10px;
    border-top: 1px solid;
    border-left: 1px solid;
    transform: rotate(225deg);
  }
  .option{
    background: #fff;
    border: 1px solid #ccc;
    border-top: none;
  }
  .option:hover{
    background-color: #ececec;
  }
</style>