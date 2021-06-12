<template>
  <div class="match">
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column type="expand">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="失主学号/工号">
              <span>{{ props.row.LosterId }}</span>
            </el-form-item>
            <el-form-item label="拾到者学号/工号">
              <span>{{ props.row.FounderId }}</span>
            </el-form-item>
            <el-form-item label="失主手机号">
              <span>{{ props.row.LosterMoblie }}</span>
            </el-form-item>
            <el-form-item label="拾到者手机号">
              <span>{{ props.row.FounderMoblie }}</span>
            </el-form-item>
            <el-form-item label="拾到时间">
              <span>{{ props.row.FoundDate }} {{ props.row.FoundTime }}</span>
            </el-form-item>
            <el-form-item label="补充信息">
              <span>{{ props.row.AdditionalInfo }}</span>
            </el-form-item>
            <el-form-item label="感谢留言">
              <span>{{ props.row.ThxMsg }}</span>
            </el-form-item>
            <el-form-item label="图片">
              <el-image
                style="width: 150px; height: 150px"
                fit="cover"
                :src="props.row.Image"
              ></el-image>
            </el-form-item>
          </el-form>
        </template>
      </el-table-column>
      <el-table-column label="失物类型" prop="ItemType"> </el-table-column>
      <el-table-column label="失物信息" prop="Info"> </el-table-column>
      <el-table-column label="失主姓名" prop="LosterName"> </el-table-column>
      <el-table-column label="拾到者姓名" prop="FounderName"> </el-table-column>
      <el-table-column label="拾到日期" prop="FoundDate"> </el-table-column>
      <el-table-column label="地点" prop="Place"> </el-table-column>
      <el-table-column label="详细地点" prop="PlaceDetail"> </el-table-column>
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
  name: "match",
  mounted() {
    this.getList();
  },
  methods: {
    getList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/match", {})
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
.match {
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
