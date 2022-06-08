<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
   
      <!-- <abc msg="aa"></abc> -->
      <myProduct v-for="(item,ind) in list" :key="item.id" 
      :title="item.proname"
      :price="item.proprice"
      :intro="item.info"
      :index="ind"
      @subprice="fn"
      ></myProduct>
    
  </div>

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import abc from './components/select11.vue'
import myProduct from './components/myProduct.vue'

export default {
  name: 'App',
  data(){
    return {
      list: [
    { id: 1, proname: "超级好吃的棒棒糖", proprice: 18.8, info: '开业大酬宾, 全场8折' },
    { id: 2, proname: "超级好吃的大鸡腿", proprice: 34.2, info: '好吃不腻, 快来买啊' },
    { id: 3, proname: "超级无敌的冰激凌", proprice: 14.2, info: '炎热的夏天, 来个冰激凌了' },
],
    }
  },
  methods: {
    fn(index,price){
      this.list[index].proprice>1&&(this.list[index].proprice=(this.list[index].proprice-price).toFixed(2))
      ;
    }
  }
  ,

  components: {
    // HelloWorld,
    // abc:abc
    myProduct
  }
}
</script>

<style>
</style>
