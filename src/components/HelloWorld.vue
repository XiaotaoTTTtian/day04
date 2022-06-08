<template>
  <div id="app">
    <div class="container">
      <!-- 顶部框模块 -->
      <div class="form-group">
        <div class="input-group">
          <h4>品牌管理</h4>
        </div>
      </div>

      <!-- 数据表格 -->
      <table class="table table-bordered table-hover mt-2">
        <thead>
          <tr>
            <th>编号</th>
            <th>资产名称</th>
            <th>价格</th>
            <th>创建时间</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="value in list" :key="value.id">
            <td> {{value.id}} </td>
            <td> {{value.name}} </td>

            <!-- 如果价格超过100，就有red这个类 -->
            <td :class="{red:value.price>100}"> {{value.price}} </td>
            <td> {{value.time | formData}} </td>
            <td><a href="#" :key="value.id" @click="delBtn(value.id)">删除</a></td>
          </tr>
        </tbody>
         
         <tfoot >
          <tr>
            <td colspan="5" style="text-align: center" v-if="list.length<=0">暂无数据</td>
          </tr>
        </tfoot> 
          
      </table>

      <!-- 添加资产 -->
      <form class="form-inline">
        <div class="form-group">
          <div class="input-group">
            <input
              type="text"
              class="form-control"
              placeholder="资产名称"
              v-model.trim="name"
            />
          </div>
        </div>
        &nbsp;&nbsp;&nbsp;&nbsp;
        <div class="form-group">
          <div class="input-group">
            <input
              type="text"
              class="form-control"
              placeholder="价格"
              v-model.number="price"
            />
          </div>
        </div>
        &nbsp;&nbsp;&nbsp;&nbsp;
        <!-- 阻止表单提交 -->
        <button class="btn btn-primary" @click="addBtn">添加资产</button>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      name: "", // 名称
      price: 0, // 价格
      list: [
        { id: 100, name: "外套", price: 199, time: new Date('2010-08-12')},
        { id: 101, name: "裤子", price: 34, time: new Date('2013-09-01') },
        { id: 102, name: "鞋", price: 25.4, time: new Date('2018-11-22') },
        { id: 103, name: "头发", price: 19900, time: new Date('2020-12-12') }
      ],
    };
  },
  methods:{
    // add the asset
    addBtn(){
      if(this.name==''||this.price===0){
        return alert('请输入商品');
      }
      // get id value
      let id=this.list.length==0?1:this.list[this.list.length-1].id+1
      this.list.push({
        id:id,
        name:this.name,
        price:this.price,
        time:new Date()
      });
      this.name='';
      this.price=0
    },
    // delete an item
    delBtn(id){
      // find index by id
      let index=this.list.findIndex(element=>element.id===id)
      this.list.splice(index,1)
    }
  },
  filters:{
    // formatting time
    formData:value=>{
             // 获取年月日时分秒值  slice(-2)过滤掉大于10日期前面的0
        var datetime =  new Date(value)
        var year = datetime.getFullYear(),
        month = ("0" + (datetime.getMonth() + 1)).slice(-2),
        date = ("0" + datetime.getDate()).slice(-2),
        hour = ("0" + datetime.getHours()).slice(-2),
        minute = ("0" + datetime.getMinutes()).slice(-2),
        second = ("0" + datetime.getSeconds()).slice(-2);
        // 拼接
        var result = year + "-"+ month +"-"+ date +" "+ hour +":"+ minute +":" + second;
        // 返回
        return result;
    }
  }

};
</script>

<style >
.red{
  color: red;
}
</style>