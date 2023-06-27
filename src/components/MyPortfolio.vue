<template>
  <div>
    <div class="portfolio-list" >
      <portfolio-item v-for="elem in portfList" :key="elem.id" :portf-item="elem" ></portfolio-item>
    </div>
  </div>

</template>

<script>
import PortfolioItem from "@/components/PortfolioItem";
export default {
  components: {PortfolioItem},
  props:{
  portfList:{
    type: Array,
    default:()=>[]
  }},
}

</script>

<style scoped>
.portfolio-list{
  display: flex;
  margin: auto;
  justify-content: space-around;
  flex-wrap: wrap;
}
</style>