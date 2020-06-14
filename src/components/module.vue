<template>
  <div class="add">
    <!-- 右边滑块 -->
    <el-drawer title="我嵌套了表格!" :visible.sync="detailR" direction="rtl" size="50%">
        滑块数据详情
    </el-drawer>
    <!-- 右边滑块end -->

    <div v-if="moduleType.type==1" class="add_item">
      <!-- <div > -->
        <div @click="detailR = true" class="item_main">
          <div class="add_header">
            <span>申请人</span>
            <img src="@/assets/logo.png" alt />
          </div>
          <div class="add_main">
            <div class="add_text">工作区域可填</div>
            <div class="add_footer">
              <div class="add_footer_left">
                <el-tooltip class="item" effect="dark" content="点击查看可编辑字段" placement="bottom-start">
                  <span>
                    <img src="@/assets/logo.png" alt />
                    2
                  </span>
                </el-tooltip>
                <el-tooltip class="item" effect="dark" content="点击查看隐藏字段" placement="bottom-start">
                  <span>
                    <img src="@/assets/logo.png" alt />
                    4
                  </span>
                </el-tooltip>
                <el-tooltip class="item" effect="dark" content="点击查看仅可见字段" placement="bottom-start">
                  <span>
                    <img src="@/assets/logo.png" alt />
                    3
                  </span>
                </el-tooltip>
              </div>
              <div class="add_footer_right">
                <el-tooltip class="item" effect="dark" content="复制节点" placement="bottom">
                  <span>
                    <img src="@/assets/logo.png" alt />
                  </span>
                </el-tooltip>
              </div>
            </div>
          </div>
        </div>
   <!-- </div> -->
      <div class="add_line">
        <el-popover :value='show' placement="right" width="200" trigger="click" visible-arrow=false>
          <ul >
            <li @click="add(1)">A1</li>
            <li @click="add(2)">B2</li>
            <li @click="add(3)">C3</li>
          </ul>
          <div class="add_add" slot="reference">+</div>
        </el-popover>
      </div>
     
    </div>
<!-- type2 -->
    <div v-if="moduleType.type==2" class="item2">
      <div class="item2_border">
          <div class="item2_add" @click="add2()">+</div>
        
          <div class="item2_item" v-for="(ele,i) in moduleType.list" :key=i >
                <div class="item2_title">所有数据可进行该分支</div>
                <div class="item2_filter">筛选数据</div>
                <el-popover placement="right" width="200" trigger="click" visible-arrow=false>
                    <ul>
                      <li @click="addz(1,i,moduleType.list)">A1</li>
                      <li @click="addz(2,i,moduleType.list)">B2</li>
                      <li @click="addz(3,i,moduleType.list)">C3</li> 
                    </ul>
                    <div class="branch_add_add" slot="reference">+</div>
                </el-popover>
                <!-- {{ele}} -->
                <div v-if=ele.type&&ele.list>
                  <module  v-for="(child,index) in ele.list" :key=index :moduleType=child :dataArr=ele.child :index=index></module>
                </div>
          </div>
        
      </div>
      <div class="add_line">
        <el-popover placement="right" width="200" trigger="click" visible-arrow=false>
          <ul>
            <li @click="add(1)">A1</li>
            <li @click="add(2)">B2</li>
            <li @click="add(3)">C3</li>
          </ul>
          <div class="add_add" slot="reference">+</div>
        </el-popover>
      </div>

    </div>
    <!-- type3 -->
    <div v-if="moduleType.type==3">C</div>
  </div>
</template>

<script>
export default {
  name: "module",
  data() {
    return {
      filter:[{list:[]},{list:[]}],
      chartData: [],//模块类型数组
      detailR: false,//右边滑块是否显示
      show:false
      // timer: null
    };
  },
  created(){
    console.log("this,dataArr",this.dataArr,'-=-=',this.index)
    if(this.dataArr){
      this.filter = this.dataArr[this.index].list
      console.log ("112",this.filter )
    }
  },
  methods: {
    add(n) {
      var obj = {
        type:n,
        list:[]
      }
      if(n==2){
        obj.list=this.filter
      }
      console.log("----",this.dataArr)
      this.dataArr.splice(this.index+1, 0, obj);
      // console.log("chartData:", this.chartData);
      // this.$emit("childByValue", this.chartData);
      // this.$refs.ul.style.display = 'none'
      // this.show = false
    },
    add2(){
      this.filter.push({list:[]})
        console.log('dataArr',this.dataArr)
         
    },
    addz(n,index,arr){
      console.log('++++++',this.filter,arr,index)
       var obj = {
         type:n,
        list:[]
      }
      if(n==2){
        obj.list=this.filter
      }
      let a = arr[index].list.splice(index, 0, obj)
      // let b = arr.splice(index+1,1 ,a)
      console.log(a ,'-=-=-=-=')
      this.dataArr.splice(this.index, 0, arr);
      console.log(JSON.stringify(this.dataArr))
    }
  },
  props: ["moduleType","dataArr","index"]//moduleType:模块类型
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped>
li {
  list-style: none;
}
.add {
  width: 100%;
  /* margin-bottom: 100px; */
  /* border: solid 2px darkorchid; */
}

.add_item {
  box-sizing: border-box;
  width: 270px;
  /* height: 120px; */
  margin: auto;
  
 
  cursor: pointer;
  /* border: solid 1px; */
}
.item_main{
   width: 270px;
  height: 120px;
  box-shadow: 0 2px 3px 0 rgba(0,0,0,.1);
   background-color: #fff;
   /* border: solid 1px red; */
}

img {
  width: 16x;
  height: 16px;
  vertical-align: center;
}

.add_header {
  height: 50px;
  line-height: 50px;
  background: -webkit-linear-gradient(
    to right,
    #324963,
    #5b6d85,
    #828fa5
  ); /* Safari 5.1-6.0 */
  background: -o-linear-gradient(
    to right,
    #324963,
    #5b6d85,
    #828fa5
  ); /* Opera 11.1-12.0 */
  background: -moz-linear-gradient(
    to right,
    #324963,
    #5b6d85,
    #828fa5
  ); /* Firefox 3.6-15 */
  background: linear-gradient(
    to right,
    #324963,
    #5b6d85,
    #828fa5
  ); /* 标准语法 */
  width: 100%;
  color: #fff;
  padding: 0 14px;
  box-sizing: border-box;
  display: flex;
  align-items: center;
}
.add_header span {
  font-size: 15px;
}
.add_header img {
  text-align: right;
  margin-left: auto;
  opacity: 0.3;
}

.add_main {
  background: white;
  color: #b0b0b9;
  padding: 0 15px;
}

.add_text {
  background: #ccc;
  font-size: 12px;
  color: #b0b0b9;
  padding: 10px 0;
  border-bottom: solid 1px #f5f5f7;
  background: white;
}

.add_footer {
  /* line-height: 40px; */
  display: flex;
  /* height: 40px; */
  color: #6b737b;
}
.add_footer span {
  display: flex;
  align-items: center;
  width: 35px;
  height: 25px;
}
.add_footer_left {
  flex-grow: 1;
  display: flex;
}
.add_footer_right {
  margin-left: auto;
}
.add_footer_right span {
  width: 25px;
  height: 25px;
  line-height: 25px;
}
.add_footer_right span img {
  margin-left: auto;
}

.add_line {
  width: 1px;
  height: 90px;
  border: solid 0.5px #dfdfe8;
  background: #dfdfe8;
  margin: auto;
  position: relative;
}

.add_add,.branch_add_add{
  position: absolute;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 30px;
  height: 30px;
  line-height: 30px;
  text-align: center;
  font-size: 20px;
  background-color: #fff;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  cursor: pointer;
  z-index: 1;
  outline: 0;
  border: none;
  color: #f5bc21;
  font-size: 22px;
  font-weight: 600;
}
.add_add:hover {
  background-color: #f5bc21;
  color: #fff;
}

/* 分支 */

 .item2{
 
   width: 500px;
 
   margin: auto;
   border: solid 1px red;
  
 }
 .item2 .add{
   margin: 0;
 }
 .item2_border{ 
   /* height: 192px; */
   position: relative;
   border: double gold 1px;
   display: flex;
 }

 .item2_add{
   position: absolute;
   left: 50%;
   transform: translate(-50%,-50%);
   width:20px;
   height: 20px;
   line-height: 19px;
   text-align: center;
   font-size: 20px;
   border: solid 1px red;
   background: yellow;
   border-radius: 50%;
 }

 

 .item2_item{
    box-shadow: 0 1px 4px 0 rgba(25,30,40,.1);
    background: white;
    width: 270px;
    height: 100px;
    border-radius: 3px;
    border: solid 1px darkgoldenrod;
    margin: 50px 0 90px;
    transform: translateX(-50%);
    position: relative;
 }

 .item2_item:last-of-type{
    transform: translateX(50%)
 }


 .item2_title{
   height: 60px;
   line-height: 60px;
   padding: 0 18px;
   border-bottom: solid 1px #ebebf0;
 }
.item2_filter{
  height: 40px;
   line-height: 40px;
   padding: 0 18px;
   color: #f5bc21;

}

.branch_add_add{
  top: 150%;
  left: 50%;
}
</style>
