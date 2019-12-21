<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="opid" label="ID" width="180"></el-table-column>
    <el-table-column prop="userId" label="用户ID" width="180"></el-table-column>
    <el-table-column prop="userName" label="用户名"></el-table-column>
    <el-table-column prop="time" label="操作时间"></el-table-column>
    <el-table-column label="操作类型">
      <template slot-scope="scope">
        <el-tag size="medium">{{ scope.row.type | Convert }}</el-tag>
      </template>
    </el-table-column>
    <el-table-column prop="money" label="操作金额"></el-table-column>
    <el-table-column prop="rest" label="账户余额"></el-table-column>
  </el-table>
</template>

<script>
export default {
  name: "deposit",
  data() {
    return {
      tableData: [
        {
          opid: "2016-05-02",
          userId: "123",
          userName: "mimi",
          time:"20190102",
          type:1,
          money:100,
          rest:300
        }
      ]
    };
  },
  filters: {
    Convert: function(value) {
      if(value == 1){
          return "存款"
      }
      else {
          return "取款"
      }
    }
  },
  methods: {

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
