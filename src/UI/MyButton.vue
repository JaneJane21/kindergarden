<template>
<button>
  <slot></slot>
</button>
</template>

<script>
export default {

}
</script>

<style scoped>
button{
  border-radius: 10px;
  border: 2px solid black;
  background-color: white;
  padding: 10px 15px;
  color: black;
  cursor: pointer;
}
button:hover{
  background-color: black;
  color: white;
}
</style>