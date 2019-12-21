<template>
  <div>
    <!-- <el-dialog title="新增业务" :visible.sync="dialogFormVisible"> -->
    <el-form :model="form" :rules="rules" ref="form">
      <el-form-item label="姓名" prop="username" :label-width="formLabelWidth">
        <el-col :span="10">
          <el-input v-model="form.username" autocomplete="off"></el-input>
        </el-col>
      </el-form-item>
      <el-form-item label="年龄" prop="age" :label-width="formLabelWidth" size="small">
        <el-col :span="10">
          <el-input-number v-model="form.age" :min="1" label="请输入年龄"></el-input-number>&nbsp;&nbsp;&nbsp;岁
        </el-col>
      </el-form-item>
      <el-form-item label="身份证号" prop="idcard" :label-width="formLabelWidth">
        <el-col :span="10">
          <el-input v-model="form.idcard" autocomplete="off"></el-input>
        </el-col>
      </el-form-item>
      <el-form-item label="银行卡号" prop="bankcard" :label-width="formLabelWidth">
        <el-col :span="10">
          <el-input v-model="form.bankcard" autocomplete="off"></el-input>
        </el-col>
      </el-form-item>
      <el-form-item label="密码" prop="password" :label-width="formLabelWidth">
        <el-col :span="10">
          <el-input v-model="form.password" autocomplete="off"></el-input>
        </el-col>
      </el-form-item>
    </el-form>
    <div style="text-align:right;">
      <el-button type="primary" @click="submit">确定</el-button>
    </div>
    <!-- <div slot="footer" class="dialog-footer">
      <el-button @click="dialogFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
    </div>-->
    <!-- </el-dialog> -->
  </div>
</template>

<script>
export default {
  name: "loan",
  data() {
    return {
      form: {
        username: "",
        age: 18,
        idcard: "",
        bankcard: "",
        password: ""
      },
      formLabelWidth: "120px",
      rules: {
        username: [{ required: true, message: "请输入姓名", trigger: "blur" }],
        idcard: [
          { required: true, message: "请输入身份证号", trigger: "change" }
        ],
        bankcard: [
          { required: true, message: "请绑定银行卡号", trigger: "change" }
        ],
        password: [{ required: true, message: "请设置密码", trigger: "change" }]
      }
    };
  },

  methods: {
    submit() {
      this.$refs["form"].validate(valid => {
        if (valid) {
          console.log("验证通过");
          this.$axios({
            method: "post",
            url: "http://localhost:8081/user",
            data: this.form
          }).then(res => {
            console.log(res.data);
            if (res.data == "OK") {
              this.$message.success("添加用户成功");
              this.reset();
              this.sendflag();
            }
          });
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    sendflag() {
      this.$emit("sendflag", false);
    },
    reset() {
      this.form = {
        username: "",
        age: 18,
        idcard: "",
        bankcard: "",
        password: ""
      };
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
