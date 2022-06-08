<template>
  <div>
    <span>全选:</span>
    <input type="checkbox" v-model="isAll" />
    <button @click="reverseBtn">反选</button>
    <ul>
      <li v-for="(value, index) in arr" :key="index">
        <input type="checkbox" v-model="value.c"/>
        <span>{{ value.name }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr: [
        {
          name: "猪八戒",
          c: false,
        },
        {
          name: "孙悟空",
          c: false,
        },
        {
          name: "唐僧",
          c: false,
        },
        {
          name: "白龙马",
          c: false,
        },
      ]
    };
  },
  methods:{
    // reverse function
    reverseBtn(){
      this.arr.forEach(item=>item.c=!item.c)
    }
  },
  computed: {
    isAll:{
      // all select affects small section
      set(value){
        this.arr.forEach(item=>item.c=value);
    },
      // small selection affects all selection
    get(){
      return this.arr.every(item=>item.c===true)
    }
  }
  }
};
</script>
<style></style>