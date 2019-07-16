<template>
  <div class="main">
    <myheader></myheader>
    <div class="digesttext"><img class="leftTopImg" src="../assets/traveldigest/zhaiyao.png" alt="">
      订单信息
    </div>
    <div v-show="!hasdata">
      未查到您的订单信息
    </div>
    <div class="digestlist" v-for="(item,i) of list" :key="i" v-show="hasdata">
      <!-- 去程航班信息 -->
      <div class="listGoText">
        <h5>航班信息</h5>
        <span class="statusText">FLEX</span>
        <div class="destination">{{item.saddr}}>{{item.taddr}}</div>
        <div class="timing"><span>出发:</span>{{item.sap}} {{item.ystime}}</div>
        <div class="timing"><span>到达:</span>{{item.tap}} {{item.yetime}}</div>
        <!-- <div class="timing"><span>转机:</span> 上海,巴黎</div> -->
      </div>
      
      <div class="borderRight"></div>
      <!-- 人数和时间 -->
      <div class="peoAndTime">
        <div>
          <span class="ss">姓名：</span>{{item.name}}
          <span class="ss ml-5">身份证号：</span>{{item.idCard}}
        </div>

        <div>
          <span class="ss">性别：</span>{{item.sex}}
          <span class="ss ml-5">订票时间：</span>{{item.ordertime}}
        </div>

        <div>
          <span class="ss">手机号：</span>{{item.phone}}
        </div>

        <div>
          <span class="ss">订单号：</span>{{item.order}}
        </div>
      </div>
      <div class="borderRight"></div>
      <!-- 价格总计 -->
      <div class="title">
        <div>含税价格总计：</div>
        <div>￥{{item.price}}元</div>
      </div>
    </div>
    <myfooter></myfooter>
  </div>
</template>
<script>
import myheader from "./common/header"
import myfooter from "./common/footer"
export default {
  data() {
    return {
      list:[],
      hasdata:false,
    }
  },
  components:{myheader,myfooter},
  created(){
    this.axios.get("/pltk/query").then((res)=>{
      if(res.data.code == 1){
        console.log(res.data.data);
        this.hasdata = true;
        for(var i=0;i<res.data.data.length;i++){
          var obj = {};
          obj.name=res.data.data[i].name;
          obj.phone=res.data.data[i].phone;
          obj.idCard=res.data.data[i].id;
          if(res.data.data[i].gender==0){
            obj.sex="女";
          }else{
            obj.sex="男";
          };
          obj.price=res.data.data[i].price;
          var ordertime=res.data.data[i].stime;
          ordertime = new Date(ordertime).toLocaleString('chinese',{hour12:false});
          obj.ordertime=ordertime;
          obj.order = res.data.data[i].tkn;
          obj.saddr = res.data.data[i].saddr;
          obj.taddr = res.data.data[i].taddr;
          obj.sap = res.data.data[i].sap;
          obj.tap = res.data.data[i].tap;
          obj.ystime = res.data.data[i].ystime;
          obj.yetime = res.data.data[i].yetime;
          this.list.push(obj);
          //console.log(this.list[i]);
        }        
      }    
    })
  }
}
</script>
<style scoped>
.leftTopImg{
  width: 45px;
  margin: 1.5rem 1.3rem;
}
.digesttext{
  font-size: 1.5rem;
  font-weight: 700;
}
.digestlist+.digestlist{
  margin-top:2rem;
}
/* 左边框线 */
.borderRight{
  border-right:0.1rem solid #bdbdbd;
}
/* 摘要详细信息 */
.digestlist{
  background-color: #dff2fd;
  color:#051039;
  box-shadow: 0 0.5rem 1rem 0 #e8e5e5;
  cursor: pointer;
  width: 100%;
  position: static;
  padding:2rem 0;
  display: flex;
  justify-content: space-around;
}
.listGoText,.listBackText{
  padding:0 2rem 0 4rem;
  max-width: 18.75rem;
}
.statusText{
  background-color: #0062e6;
  color:#fff;
  font-weight: 700;
  padding:0.3rem 0.75rem;
  display: inline-block;
  margin-bottom: 0.75rem;
}
.destination{
  color:#dc0000;
  font-weight: 700;
  font-size: 1.3rem;
}
.timing>span{
  font-weight:bolder;
  margin-bottom: 10px;
}
.peoAndTime{
  padding:0 2rem;
}
.peoAndTime div{
  margin:0.5rem 0;
}
.title{
  vertical-align: middle;
  padding-right:4rem;
  color: #051039;
}
.title>div{
  font-size: 1.3rem;
  font-weight: bolder;
}
.ss{
  font-size:1.1rem;
  font-weight:700 !important;
}
</style>