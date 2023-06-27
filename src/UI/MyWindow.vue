<template>
  <div class="dialog" v-if="display" @click.stop="this.$emit('update:display',false)">
    <div class="content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    display:{
      type:Boolean,
      default:false
    }
  }
}
</script>

<style scoped>
.dialog{
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0,0,0,0.5);
  position: fixed;
  display: flex;
  z-index: 100;
}
.content{
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 50px;
  min-width: 300px;
}
</style>