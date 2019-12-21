<template>
 <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        prop="id"
        label="用户ID"
        width="180">
      </el-table-column>
      <el-table-column
        prop="username"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="password"
        label="密码">
      </el-table-column>
    </el-table>
</template>

<script>
export default {
  name: "user",
      data() {
        return {
          tableData: [{
            id: '2019122001',
            username: '王小虎',
            password: 'wxh666'
          }, {
            id: '2019122002',
            username: '秘秘秘秘',
            password: 'lqm990328'
          }]
        }
      },
  methods: {

  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
