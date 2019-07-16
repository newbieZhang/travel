<template>
  <div>
    <button @click="getuser">加载数据</button>
    <table class="table">
      <tr class="row">
        <td>用户id</td>
        <td>用户名</td>
        <td>用户密码</td>
        <td>用户订单</td>
        <td>删除用户</td>
        <td>修改用户</td>
      </tr>
      <tr class="row" v-for="(item,index) of list" :key="index">
        <td>{{item.uid}}</td>
        <td>{{item.uname}}</td>
        <td>{{item.upwd}}</td>
        <td>qweqwe123132</td>
        <td> 
          <button @click="del(item.uid)">删除用户</button>
        </td>
        <td>
          <button @click="change">修改用户信息</button>
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  data(){
    return {
      list:[],
      uid:'',
    }
  },
  methods:{
    // 读取用户资料
    getuser(){
      this.axios.get('/user/selectall').then(res=>{
        this.list=res.data.data;
      })
    },
    // 删除用户
    del(){
      this.uid=item.uid
      this.axios.get("/user/del",{params:{uid:uid}}).then(res=>{
        if(res.data.code==1){
          alert("删除成功");
        }else{
          alert("删除失败");
        }
      })
    },
    // 修改用户资料
    change(){
      console.log(123);
    },
    created() {
      this.getuser()
    },
  }
}
</script>
<style scoped>
.table{
  width: 95%;
  border: 0;
  margin: 0 auto;
}
.row{
  width: 100%;
}
.row td{
  width: 16%;
  border: 1px solid #000;
}
</style>

