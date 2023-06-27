<template>
  <div>
    <select @change="changeOption" :value="modelValue">
      <option value="none" disabled selected>Сортировать по дате</option>
      <option v-for="option in options" :value="option.value" :key="option.value">{{option.name}}</option>
    </select>
  </div>
</template>

<script>
export default {
  props:{
    modelValue:{
      type: String
    },
    options:{
      type:Array,
      default:()=>[]
    }
  },
  methods:{
    changeOption(event){
      this.$emit('update:modelValue',event.target.value)
    }
  }
}
</script>

<style scoped>
select{
  background-color: white;
  border: 4px solid #FEF600;
  border-radius: 10px;
  padding: 10px 5px;
}
*, select:focus {
  outline: none !important;
}
</style>