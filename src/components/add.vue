<template>
  <div class="add">
    <!-- <el-button type="text" @click="table = true">打开嵌套表格的 Drawer</el-button> -->

    <el-drawer title="我嵌套了表格!" :visible.sync="table" direction="rtl" size="50%">
      <el-table :data="gridData">
        <el-table-column property="date" label="日期" width="150"></el-table-column>
        <el-table-column property="name" label="姓名" width="200"></el-table-column>
        <el-table-column property="address" label="地址"></el-table-column>
      </el-table>
    </el-drawer>

    <div v-if="items==1" class="add_item">
      <!-- <el-button type="text" @click="table = true"> -->
      <div @click="table = true">
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

      <div class="add_line">
        <!-- <div class="add_add">+</div> -->
        <el-popover placement="right" width="200" trigger="click" visible-arrow=false>
          <ul>
            <li @click="add(1)">A1</li>
            <li @click="add(2)">B2</li>
            <li @click="add(3)">C3</li>
          </ul>
          <div class="add_add" slot="reference">+</div>
          <!-- <el-button >click 激活</el-button> -->
        </el-popover>
      </div>
      <!-- </el-button> -->
    </div>

    <div v-if="items==2" class="item2" ref="item2">
      <div class="item2_border">
        <div class="item2_add" @click="add2()">+</div>
        <div class="item2_break">
          <div class="item2_item" v-for="(ele,i) in filter" :key=i >
            <div class="item2_line"></div>
            <div class="item2_title">所有数据可进行该分支</div>
            <div class="item2_filter">筛选数据</div>
            <div class="add_line">
              <div class="add_add">+</div>
            </div>
          </div>
        </div>
      </div>
      <div class="add_line">
        <div class="add_add">+</div>
      </div>
    </div>
    <div v-if="items==3">C</div>
  </div>
</template>

<script>
export default {
  name: "add",
  data() {
    return {
      filter:[1,1],
      chartData: [],
      table: false,
      dialog: false,
      loading: false,
      gridData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄"
        }
      ],
      timer: null
    };
  },
  methods: {
    add(n) {
      console.log(this.dataArr,'-=-=-',this.index)
      this.dataArr.splice(this.index, 0, n);
      console.log("chartData:", this.chartData);
      this.$emit("childByValue", this.chartData);

    },
    add2(){
      this.filter.push(2)
      this.$refs.item2 = ''
    }
  },
  created(){
    console.log(this.dataArr)
  },
  props: ["items","dataArr","index"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped>
li {
  list-style: none;
}
.add {
  width: 100%;
  margin-bottom: 100px;
}

.add_item {
  box-sizing: border-box;
  width: 270px;
  height: 120px;
  margin: auto;
  background-color: #fff;
  box-shadow: 0px 6px 2px 2px rgba(0, 0, 0, 0.1);
  cursor: pointer;
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
  line-height: 40px;
  display: flex;
  height: 40px;
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

.add_add {
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



 .item2{
   border-bottom: solid 1.5px #dfdfe8;
   border-top: solid 1.5px #dfdfe8;
   width: 500px;
   height: 191px;
   margin: auto;
 }
 
 .item2_border{
   
   height: 192px;
  border: solid 1px #5b6d85;
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

 .item2_break{
   width: 100%;
   height: 70px;
   /* border: solid 1px red; */
   position: absolute;
 }

 .item2_item{
   border: solid 1px #dfdfe8;

   background: red;
    width: 270px;
    height: 70px;
    position: absolute;
    top:30px;
 }
 .item2_item:first-of-type{
   transform: translateX(-50%)
 }
 .item2_item:last-of-type{
   right:0;
   transform: translateX(50%)
 }

 .item2_line {
  display: block;
  width: 1px;
  height: 31px;
  border-left: solid 1.5px #dfdfe8;
  margin-left: 50%;
  position: absolute;
  top:-32px;
}
 .item2_title{
   line-height: 40px;
 }
.item2_filter{
   line-height: 31px;

}
</style>
