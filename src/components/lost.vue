<template>
  <div class="lost">
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column type="expand">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="学号/工号">
              <span>{{ props.row.Student_Teacher_Id }}</span>
            </el-form-item>
            <el-form-item label="手机号">
              <span>{{ props.row.Moblie }}</span>
            </el-form-item>
            <br>
            <el-form-item label="可能丢失地点">
              <span>{{ props.row.Place1 }} </span>|
              <span> {{ props.row.Place2 }} </span>|
              <span> {{ props.row.Place3 }}</span>
            </el-form-item>
          </el-form>
        </template>
      </el-table-column>
      <el-table-column label="失主姓名" prop="Name"> </el-table-column>
      <el-table-column label="失物类型" prop="SubType"> </el-table-column>
      <el-table-column label="丢失日期" prop="LostDate"> </el-table-column>
      <el-table-column label="时间段" prop="LostTimeSession"> </el-table-column>
      <el-table-column label="校区" prop="Campus"> </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <!-- <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button> -->
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)"
            >删除</el-button
          >
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  name: "lost",
  mounted(){
    this.getList();
  },
  methods:{
    getList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/lost", {

        })
        .then((res) => {
          if (res.data.code == 200) {
            this.tableData = res.data.data;
          } else {
            this.$notify.error({
              title: "错误" + res.data.code,
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
    handleEdit(index, row) {
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index, row);
    },
  },
  data() {
    return {
      tableData: [],
    };
  },
};
</script>
<style scoped>
.lost {
  margin: 0;
  margin-left: 250px;
}
.demo-table-expand {
  font-size: 0;
}
.demo-table-expand label {
  width: 90px;
  color: #99a9bf;
}
.demo-table-expand .el-form-item {
  margin-right: 0;
  margin-bottom: 0;
  width: 50%;
}
</style>
