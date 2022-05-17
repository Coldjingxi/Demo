<template>
  <div class="hello">
    <el-button size="mini" @click="Add()"
      >增加</el-button
    >
    <el-table
      size="small"
      :data="userData"
      height="520"
      element-loading-text="拼命加载中"
      style="width: 100%"
      :header-cell-style="{
        'background-color': '#eee',
        height: '1.56vw',
        padding: '0',
        border: 'none',
        'font-size': '0.6vw',
        color: '#000',
      }"
    >
      <el-table-column
        align="center"
        sortable
        prop="name"
        label="姓名"
        min-width="200"
      >
      </el-table-column>
      <el-table-column
        align="center"
        sortable
        prop="sex"
        label="性别"
        min-width="200"
      >
      </el-table-column>
      <el-table-column
        align="center"
        sortable
        prop="phone"
        label="电话"
        min-width="200"
      >
      </el-table-column>

      <el-table-column label="操作" min-width="400" align="center">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
            >编辑</el-button
          >
          <el-button
            size="mini"
            type="danger"
            @click="deleteUser(scope.$index, scope.row)"
            >删除</el-button
          >
        </template>
      </el-table-column>
    </el-table>
    <!--sync必须加不然子组件监听不到  -->
    <Dialog
      :title="title"
      :QualityDialogFlag.sync="QualityDialogFlag"
      :formData.sync="formData"
      @childByValue="childByValue"
    ></Dialog>
  </div>
</template>

<script>
import Dialog from "../components/dialog.vue";
export default {
  name: "Table",
  props: {
    userData: Array,
  },
  components: { Dialog },

  data() {
    return {
      QualityDialogFlag: false, //控制编辑页面显示与隐藏
      title: "",
      formData: {},
    };
  },
  methods: {
    Add(){
      this.formData = {};
      this.QualityDialogFlag = true;
      this.title = "新增";
    },
    handleEdit(index, row) {
      console.log(index, row);
      /* 回显数据 */
      this.formData = row;
      this.QualityDialogFlag = true;
      this.title = "编辑";
    },

    /* 弹窗返回参数 */
    childByValue(childValue) {
      console.log(childValue);
      if (this.title == "新增") {
        this.userData.push(childValue)
      }
      this.QualityDialogFlag = false;
    },
    /* 删除 */
    deleteUser(index, row) {
      console.log(index, row, "index");
      this.userData = this.userData.splice(index, 1);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
