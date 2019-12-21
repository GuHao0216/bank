<template>
  <div>
    <!-- <el-dialog title="新增业务" :visible.sync="dialogFormVisible"> -->
    <el-form :model="form">
      <el-form-item label="用户ID" :label-width="formLabelWidth">
        <el-col :span="10">
          <el-input v-model="form.userid" autocomplete="off"></el-input>
        </el-col>
      </el-form-item>
      <el-form-item label="操作类型" :label-width="formLabelWidth">
        <el-radio v-model="form.type" :label="1">存款</el-radio>
        <el-radio v-model="form.type" :label="2">取款</el-radio>
        <el-radio v-model="form.type" :label="3">贷款</el-radio>
        <el-radio v-model="form.type" :label="4">还款</el-radio>
      </el-form-item>
      <el-form-item label="操作金额" :label-width="formLabelWidth" size="small">
        <el-input-number v-model="form.money" :min="1" label="请输入金额"></el-input-number>&nbsp;&nbsp;&nbsp;元
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
        type: 1,
        money: 100,
        userid: ""
      },
      formLabelWidth: "120px"
    };
  },

  methods: {
    submit() {
      if (this.form.userid == "") {
        this.$message.warning("请输入用户ID");
      } else {
        this.form.userid = parseInt(this.form.userid);
        if (this.form.type == 1 || this.form.type == 2) {
          this.$axios({
            method: "post",
            url: "http://localhost:8081/access",
            data: this.form
          }).then(res => {
            console.log(res.data);
            if (res.data == "OK") {
              this.$message.success("添加存取款业务成功");
              this.reset();
              this.sendflag();
            }
          });
        } else {
          this.form.type = this.form.type - 2;
          this.$axios({
            method: "post",
            url: "http://localhost:8081/loan",
            data: this.form
          }).then(res => {
            console.log(res.data);
            if (res.data == "OK") {
              this.$message.success("添加贷还款业务成功");
              
              this.sendflag();
              this.reset();
            }
          });
        }
      }
    },
    reset() {
      this.form = {
        type: 1,
        money: 100,
        userid: ""
      };
    },
    sendflag() {
      this.$emit("sendflag", false);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
