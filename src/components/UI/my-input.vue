<template>
  <input :value="modelValue" @input="updateInput" class="input" :type="type">
</template>

<script>
export default {
  name: "my-input",
  props:{
    type:{
      type:String,
      required:false,
      default:'text'
    },
    modelValue:{
      type:[String,Number]
    }
  },
  methods:{
    updateInput(e){
      this.$emit('update:modelValue',e.target.value)
    }
  }
}
</script>

<style scoped>

.input{
  padding: 10px;
  border:1px solid teal;
  color:teal;
  display: block;
  width: 100%;
  margin: 10px 0;
  outline: none;
}
</style>