<template>
  <section class="container">
    <ul>
      <li v-for="item in firms">
        {{item.name}}
      </li>
    </ul>
  </section>
</template>
<script>
import axios from 'axios'
export default{
  async asyncData({}){
    let { data } = await axios.get('http://m.maizuo.com/v4/api/billboard/home?__t='+(new Date())*1)
    return {firms:data.data.billboards}
  },
  head(){
    return {
      title:this.firms[0].name
    }
  }
}
</script>
<style scoped>
.title
{
  margin: 50px 0;
}
</style>
