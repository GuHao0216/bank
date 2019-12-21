<template>
  <el-table :data="tableData" style="width: 100%">
    <el-table-column prop="opid" label="ID" width="180"></el-table-column>
    <el-table-column
      prop="userid"
      :filters="idList"
      :filter-method="filterHandler"
      label="用户ID"
      width="180"
    ></el-table-column>
    <el-table-column prop="username" label="用户名"></el-table-column>
    <el-table-column label="操作时间">
      <template slot-scope="scope">{{scope.row.time | timeFilter}}</template>
    </el-table-column>
    <el-table-column label="操作类型">
      <template slot-scope="scope">
        <el-tag
          :type="scope.row.type === 1 ? 'primary' : 'success'"
          size="medium"
        >{{ scope.row.type | Convert }}</el-tag>
      </template>
    </el-table-column>
    <el-table-column prop="money" label="操作金额"></el-table-column>
    <el-table-column prop="rest" label="账户余额"></el-table-column>
  </el-table>
</template>

<script>
export default {
  name: "deposit",
  props: ["tableData"],
  data() {
    return {
      idList: []
    };
  },
  filters: {
    Convert: function(value) {
      if (value == 1) {
        return "存款";
      } else {
        return "取款";
      }
    },
    timeFilter: function(value) {
      var str = value;
      str = str.split(".")[0];
      str = str.replace(/T/, " ");
      // alert(str);
      return str;
    }
  },
  methods: {
    initIdList() {
      // console.log(this.tableData);
      this.tableData.forEach(
        function(item) {
          var obj = {
            text: item.userid,
            value: item.userid
          };
          this.idList.push(obj);
          // console.log(this.idList)
        }.bind(this)
      );
      console.log(this.idList);

      let newArr = [];
      let obj = {};
      for (var i = 0; i < this.idList.length; i++) {
        if (!obj[this.idList[i].text]) {
          newArr.push(this.idList[i]);
          obj[this.idList[i].text] = true;
        }
      }

      this.idList = newArr;
    },
    filterHandler(value, row, column) {
      const property = column["property"];
      return row[property] === value;
    }
  },
  mounted() {
    setTimeout(() => {
      this.initIdList();
    }, 2000);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
