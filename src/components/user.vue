<template>
  <div>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column prop="id" label="用户ID" width="180"></el-table-column>
      <el-table-column prop="username" label="姓名" width="180"></el-table-column>
      <el-table-column prop="age" label="年龄" width="180"></el-table-column>
      <el-table-column prop="idcard" label="身份证号" width="180"></el-table-column>
      <el-table-column prop="bankcard" label="银行卡号" width="180"></el-table-column>
      <el-table-column prop="password" label="密码"></el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button size="mini" @click="handleEdit(scope.row)">编辑</el-button>
          <el-button size="mini" type="danger" @click="handleDelete(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="编辑用户" :visible.sync="dialogFormVisible">
      <el-form :model="form" :rules="rules" ref="form">
        <el-form-item label="用户ID" :label-width="formLabelWidth">
          <el-input v-model="form.id" autocomplete="off" disabled></el-input>
        </el-form-item>
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
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="submit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "user",
  props: ["tableData"],
  data() {
    return {
      id:"",
      url:"",
      formLabelWidth: "120px",
      dialogFormVisible: false,
      form: {
        id: "",
        username: "",
        age: 1,
        idcard: "",
        bankcard: "",
        password: ""
      },
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
    handleEdit(row) {
      console.log(row);
      this.form = row;
      this.dialogFormVisible = true;
      this.id = row.id
    },
    handleDelete(row) {
      this.id = row.id
       this.url = "http://localhost:8081/user/" +this.id
       this.$axios({
            method: "delete",
            url: this.url
          }).then(res => {
            console.log(res.data);
            if (res.data == "OK") {
              this.$message.success("删除成功");
              this.reset();
              this.sendflag();
            }
          });
    },
    submit() {
      this.$refs["form"].validate(valid => {
        if (valid) {
          this.url = "http://localhost:8081/user/" +this.id
          console.log("验证通过");
          this.$axios({
            method: "put",
            url: this.url,
            data: this.form
          }).then(res => {
            console.log(res.data);
            if (res.data == "OK") {
              this.$message.success("修改成功");
              this.dialogFormVisible = false
              this.reset();
              
            }
          });
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
        sendflag() {
      this.$emit("senduserflag");
    },
    reset() {
      this.form = {
        username: "",
        age: 18,
        idcard: "",
        bankcard: "",
        password: ""
      };
    },
    cancel(){
      this.dialogFormVisible = false
      this.reset()
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
