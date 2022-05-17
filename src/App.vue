<template>
  <div id="app">
    <div class="searchBox">
      <el-input
        size="small"
        v-model="searchValue"
        auto-complete="off"
        placeholder="请输入姓名"
      ></el-input>
      <el-button size="mini" @click="search()" class="addButton"
        >搜索</el-button
      >
    </div>
    <el-button size="mini" @click="add()" class="addButton">增加</el-button>
    <Table
      :userData.sync="userData"
      @changeData="changeData"
      @editData="editData"
    ></Table>
    <Dialog
      :title="title"
      :qualityDialogFlag.sync="qualityDialogFlag"
      :formData.sync="formData"
      @childByValue="childByValue"
    ></Dialog>
  </div>
</template>

<script>
import Dialog from "../src/components/dialog.vue";
import Table from "../src/components/table.vue";
export default {
  name: "App",
  components: { Table, Dialog },
  data() {
    return {
      userData: [
        {
          name: "小虎",
          sex: "男",
          phone: "111111111111",
          id: 1,
        },
        {
          name: "小红",
          sex: "男",
          phone: "111111111111",
          id: 2,
        },
        {
          name: "小李",
          sex: "男",
          phone: "111111111111",
          id: 3,
        },
        {
          name: "王小虎",
          sex: "男",
          phone: "111111111111",
          id: 4,
        },
      ],
      searchValue: "", //搜索条件
      qualityDialogFlag: false, //控制编辑页面显示与隐藏
      title: "",
      formData: {},
    };
  },
  methods: {
    /* 搜索 */
    search() {
      var cardNumArr = [];
      //定义一个空的数组
      var searchRow = {};
      //定义一个空的对象

      searchRow = this.userData.find(
        (item) => item.name == this.searchValue
      );
      cardNumArr.push(searchRow);
      
      this.userData = cardNumArr
    },
    /* 编辑 */
    editData(row) {
      /* 回显数据 */
      this.qualityDialogFlag = true;
      this.formData = row;
      this.title = "编辑";
    },

    /* 删除选中行 */
    changeData(index) {
      this.userData.splice(index, 1);
    },
    /* 添加 */
    add() {
      this.qualityDialogFlag = true;
      this.title = "添加";
    },
    /* 处理弹窗返回的参数 */
    childByValue(childValue) {
      if (this.title == "添加") {
        this.userData.push(childValue);
        this.qualityDialogFlag = false;
        this.formData = {};
      }
      this.qualityDialogFlag = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.addButton {
  float: right;
}
.searchBox {
  width: 200px;
  float: left;
  display: flex;
}
</style>
