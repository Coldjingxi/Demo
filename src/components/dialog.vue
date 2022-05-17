<template>
  <div>
    <!-- 编辑界面 -->
    <el-dialog
      :title="title"
      :visible.sync="visible"
      :close-on-click-modal="false"
      @close="qualityDialogClose"
    >
      <el-form
        label-width="80px"
        ref="editForm"
        :model="editForm"
        :rules="rules"
      >
        <el-form-item label="姓名" prop="name">
          <el-input
            size="small"
            v-model="editForm.name"
            auto-complete="off"
            placeholder="请输入姓名"
          ></el-input>
        </el-form-item>
        <el-form-item label="性别" prop="sex">
          <el-input
            size="small"
            v-model="editForm.sex"
            auto-complete="off"
            placeholder="请输入用户名"
          ></el-input>
        </el-form-item>
        <el-form-item label="手机号" prop="phone">
          <el-input
            size="small"
            v-model="editForm.phone"
            placeholder="请输入手机号"
          ></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button size="small" @click="qualityDialogClose">取消</el-button>
        <el-button size="small" type="primary" @click="submitForm('editForm')"
          >保存</el-button
        >
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "Dialog",
  props: {
    /* 子组件不能直接操作父组件传递过来的参数 */
    qualityDialogFlag: Boolean,
    title: String,
    formData: Object,
  },

  watch: {
    formData() {
      this.editForm = this.formData;
    },
    /* 监听变量赋值 子组件不能直接改变父组件参数 会报错 */
    qualityDialogFlag() {
      this.visible = this.qualityDialogFlag;
    },
  },

  data() {
    return {
      visible: false,
      editForm: {
        name: "",
        sex: "",
        phone: "",
      },
      rules: {
        sex: [{ required: true, message: "请输入性别", trigger: "blur" }],
        name: [{ required: true, message: "请输入姓名", trigger: "blur" }],
        phone: [
          { required: true, message: "请输入手机号", trigger: "blur" },
          {
            pattern: /^1(3\d|47|5((?!4)\d)|7(0|1|[6-8])|8\d)\d{8,8}$/,
            required: true,
            message: "请输入正确的手机号",
            trigger: "blur",
          },
        ],
      },
    };
  },
  methods: {
    submitForm() {
      let that = this
      this.$refs["editForm"].validate((valid) => {
        
        if (valid) {
          // 请求方法
           that.$emit("childByValue", this.editForm);
          
        } else {
          return false;
        }
      });
     
    },
    qualityDialogClose() {
      this.$emit("update:qualityDialogFlag", false);
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
