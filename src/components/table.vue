<template>
  <div class="hello">
    
    <el-table
      size="small"
      :data="tableValue"
      height="520"
      element-loading-text="拼命加载中"
      style="width: 100%"
      :header-cell-style="headerStyle"
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
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)" >
            编辑
          </el-button>
           
          <el-button
            size="mini"
            type="danger"
            @click="deleteUser(scope.$index, scope.row)" >
            删除
          </el-button> 
          
        </template>
      </el-table-column>
    </el-table>
    <!--sync必须加不然子组件监听不到  -->
    
  </div>
</template>

<script>

export default {
  name: "Table",
  props: {
    userData: Array,
  },
  created(){
    this.tableValue = this.userData;
  },
  watch: {
    userData() {
      this.tableValue = this.userData;
    },
  },
  data() {
    return {
      tableValue: [],
      headerStyle:{
        'background-color': '#eee',
        height: '1.56vw',
        padding: '0',
        border: 'none',
        'font-size': '0.6vw',
        color: '#000',
      }
    };
  },
  methods: {
    /* 编辑 */
    handleEdit(index, row) {
      console.log(index, row);
      /* 回显数据 */
      
       this.$emit("editData",row);
    },

    /* 弹窗返回参数 */
    childByValue() {
      
      this.qualityDialogFlag = false;
    },
    /* 删除 */
    deleteUser(index) {
      this.$confirm(`确定要删除该数据吗？`, {
                type: "warning",
                //beforeClose 阻止关闭弹窗
                beforeClose: (action, instance, done) => {
                    //下面这行代码就是弹出的确认删除和取消删除
                    if (action === "confirm") {
                        this.$emit("changeData",index);
                        done();
                    } else {
                        //点击其他地方时就相当于点击了false
                        done();
                    }
                },
            });
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
