<template>
  <div class="hello">
  <el-table
      size="small"
      @selection-change="selectChange"
      :data="userData"
      height="520"
      v-loading="loading"
      element-loading-text="拼命加载中"
      style="width: 100%"
      :row-class-name="tableRowClassName"
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
          <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
            >增加</el-button
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
  </div>
</template>

<script>
export default {
  name: 'Table',
  props: {
    userData: Array
  }
  
}
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
