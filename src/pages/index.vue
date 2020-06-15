<template>
  <div class="flowPath" >
    <!-- <div class="add_btn" @click=add(1)>+</div>
    <div class="add_btn" @click=add(2)>+</div> -->
    <!-- <module :moduleType=1 :dataArr=data :index=0></module> -->
    <div class="top">
      <div>上传</div>
      <div @click="fd" class="fd">+</div>
      <div class="ratio">{{(ratio*100).toFixed(0)}}%</div>
      <div @click="sx" class="sx">-</div>
    </div>
    <div id="view" ref='view'>
       <!-- <module v-for="(item,index) in data" :key="index" :moduleType=item :dataArr=data :index=index></module> -->
       <add v-for="(item,index) in data" :key="index" :moduleType=item :dataArr=data :index=index></add>

      <div class="end">
        <div class="end_btn">结束</div>
      </div>
    </div>
    
  </div>
</template>

<script>
import module from "../components/module"
import add from "../components/add"
// import set from "../components/set"
export default {
  name: '',
  data () {
    return {
      data:[
        { type:1,list:[]},
        { type:2,list:[{type:1,list:[]},{type:2,list:[]}]}
        // { type:2,list:[{type:1,list:[{type:1,list:[]},{type:1,list:[]}]},{type:2,list:[]}]}
      ],
      ratio:1,//放大缩小比例,
      // a:0
    } 
  },
  components:{
    module,
    add
    // set
  },
  created(){
   
  },
  methods:{
    // add(n){
    //   this.data.push(n)
    // },
     childByValue(childValue) {  // childValue就是子组件传过来的值
        console.log("-----childValue:",childValue)
        this.data = childValue
   },
   fd(){
      console.log("-----------放大:",this.ratio)
      if(this.ratio-0<2){
          this.ratio=(this.ratio-0+0.1).toFixed(2)
          console.log("放大比例:",this.ratio)
          this.$refs.view.style.transform ='scale('+this.ratio+')'
      }
     

   },
    sx(){
     console.log("-----------缩小:",this.ratio)
      if(this.ratio-0>0.5){
          this.ratio=(this.ratio-0-0.1).toFixed(2)
          console.log("缩小比例:",this.ratio)
          
          this.$refs.view.style.transform ='scale('+this.ratio+')'
      }
     
   }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.flowPath{
  font-size: 14px;
  border: solid 2px darkcyan;
  background: #f5f5f7;
  /* height: 100vh;
  overflow-y:scroll; */
  padding: 50px 0;
  
}
.top{
  display: flex;
  border: solid 1px;
  position: fixed;
  right: 20px;
  top: 20px;
  z-index: 100;
}
.fd,.sx{
  width: 30px;
  height: 30px;
  text-align: center;
  line-height: 30px;
  background: darkgrey;
  border-radius: 3px;

}
.ratio{
   width: 50px;
  height: 30px;
   text-align: center;
    line-height: 30px;
  overflow: hidden;
}
      
/* .add_btn{
  width: 20px;
  height: 20px;
  background: orange;
  text-align: center;
  
} */

.end_btn{
    width: 50px;
    height: 50px;
    background: linear-gradient(-120deg,#dfdfe8 1%,#afafb8 100%);
    box-shadow: 0 1px 5px 0 rgba(0,0,0,.2);
    border-radius: 100%;
    color: #fff;
    text-align: center;
    line-height: 50px;
    margin: auto;
    box-sizing: border-box;
    
}
</style>
