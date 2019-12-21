<template>
  <div>
    <div style="text-align:center">
      <el-button @click="userFormVisible = true" style=" align: center;">新增用户</el-button>
      <el-button @click="bankFormVisible = true" style=" align: center;">新增业务</el-button>
    </div>
    <div v-if="bankFormVisible">
      <el-dialog :visible.sync="bankFormVisible" width="35%" title="新增业务">
        <bankform :visible.sync="bankFormVisible" @sendflag="getbankFlag"></bankform>
      </el-dialog>
    </div>
    <div v-if="userFormVisible">
      <el-dialog :visible.sync="userFormVisible" width="35%" title="新增用户">
        <userform :visible.sync="userFormVisible" @sendflag="getuserFlag"></userform>
      </el-dialog>
    </div>
    <el-tabs v-model="activeName">
      <el-tab-pane label="用户管理" name="first">
        <user :tableData="userdata" @senduserflag="init"></user>
      </el-tab-pane>
      <el-tab-pane label="存取款管理" name="third">
        <deposit :tableData="assessdata"></deposit>
      </el-tab-pane>
      <el-tab-pane label="贷还款管理" name="fourth">
        <loan :tableData="loandata"></loan>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import user from "./user";
import userform from "./userform";
import bankform from "./bankform";
import deposit from "./deposit";
import loan from "./loan";
export default {
  name: "bank",
  data() {
    return {
      userdata: [],
      assessdata: [],
      loandata:[],
      activeName: "first",
      userFormVisible: false,
      bankFormVisible: false
    };
  },
  components: {
    user,
    deposit,
    loan,
    bankform,
    userform
  },
  methods: {
    init() {
      const url = "http://localhost:8081/user";

      this.$axios
        .get(url)
        .then(response => {
          console.log(response.data);
          this.userdata = response.data;
        })
        .catch(response => {
          alert("请求失败");
        });

      const accessUrl = "http://localhost:8081/access";
      this.$axios
        .get(accessUrl)
        .then(response => {
          console.log(response.data);
          this.assessdata = response.data;
        })
        .catch(response => {
          alert("请求失败");
        });
      const loanUrl = "http://localhost:8081/loan";
      this.$axios
        .get(loanUrl)
        .then(response => {
          console.log(response.data);
          this.loandata = response.data;
        })
        .catch(response => {
          alert("请求失败");
        });
    },
    getuserFlag(flag) {
      this.userFormVisible = flag;
      this.init();
    },
    getbankFlag(flag) {
      this.bankFormVisible = flag;
      this.init();
    }
  },
  mounted() {
    this.init();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
