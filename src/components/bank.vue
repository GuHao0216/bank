<template>
  <div>
    <el-button>新增业务</el-button>
    <el-tabs v-model="activeName" >
      <el-tab-pane label="用户管理" name="first">
        <user></user>
      </el-tab-pane>
      <!-- <el-tab-pane label="银行卡管理" name="second">
        <card></card>
      </el-tab-pane> -->
      <el-tab-pane label="存取款管理" name="third">
        <deposit></deposit>
      </el-tab-pane>
      <el-tab-pane label="贷款管理" name="fourth">
        <loan></loan>
      </el-tab-pane>
      
    </el-tabs>
  </div>
</template>

<script>
import user from './user'
// import card from './card'
import deposit from './deposit'
import loan from './loan'
export default {
  name: "bank",
  data() {
    return {
      activeName: "first"
    };
  },
  components:{
    user,deposit,loan
  },
  methods: {

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
