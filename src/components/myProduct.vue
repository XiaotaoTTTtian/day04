<template>
  <div class="my-product">
     
    <h3>标题: {{ title }}</h3>
    <p>价格: {{ price }}元</p>
    <p>{{ intro }}</p>
    <button @click="btn" >砍一刀</button>
  </div>
</template>

<script>
export default {
   //PS：props与data，computed都是变量，所以可以在上方通过插值表达式显示
  props: ['title', 'price', 'intro','index'],
  methods: {
      btn(){
          console.log(this.index);
          this.$emit('subprice',this.index,1)
      }
  }
}
</script>

<style>
.my-product {
  width: 400px;
  padding: 20px;
  border: 2px solid #000;
  border-radius: 5px;
  margin: 10px;
}
</style>