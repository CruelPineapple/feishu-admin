<template>
  <div id="item-list">
    <el-dialog
      :show-close="false"
      title="提示"
      :visible="dialogVisible"
      width="30%"
    >
      <span>请选择删除方式</span>
      <span slot="footer" class="dialog-footer">
        <el-button type="danger" @click="subDel(delBuff)">删除物品</el-button>
        <el-button type="danger" @click="mainDel(delBuff)"
          >删除物品种类</el-button
        >
        <el-button @click="dialogVisible = false">取消</el-button>
      </span>
    </el-dialog>
    <el-dialog
      :show-close="false"
      title="提示"
      :visible="dialogVisible2"
      width="30%"
    >
      <span>请选择修改目标</span>
      <el-input
        style="margin-top: 14px"
        v-model="editName"
        placeholder="新名称"
      ></el-input>
      <span slot="footer" class="dialog-footer">
        <el-button type="danger" @click="subEdit(editBuff)"
          >修改物品名称</el-button
        >
        <el-button type="danger" @click="mainEdit(editBuff)"
          >修改大类物品</el-button
        >
        <el-button @click="dialogVisible2 = false">取消</el-button>
      </span>
    </el-dialog>
    <div class="table-container">
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column label="大类物品" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.BigName }}</span>
          </template>
        </el-table-column>
        <el-table-column label="物品名称" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.SmallName }}</span>
          </template>
        </el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
              >编辑</el-button
            >
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
  </div>
</template>
<script>
export default {
  name: "itemlist",
  mounted() {
    this.getList();
  },
  data() {
    return {
      editName: "",
      dialogVisible2: false,
      editBuff: undefined,
      dialogVisible: false,
      delBuff: undefined,
      tableData: [],
    };
  },
  methods: {
    getList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/typesmall")
        .then((res) => {
          if (res.data.code == 200) {
            this.tableData = res.data.data;
          } else {
            this.$notify({
              title: "错误",
              message: "获取列表失败" + res.data.msg,
              offset: 100
            });
          }
        });
    },
    handleDelete(index, row) {
      console.log(index, row);
      this.dialogVisible = true;
      this.delBuff = row;
    },
    handleEdit(index, row) {
      console.log(index, row);
      this.dialogVisible2 = true;
      this.editBuff = row;
    },
    subEdit: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/edittypesmall", {
          params: {
            key: row.Key,
            name: this.editName,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"修改成功！",
              offset:80
            });
            this.dialogVisible2 = false;
            this.getList();
          } else {
            this.$notify({
              title: "修改失败",
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
    mainEdit: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/edittypebig", {
          params: {
            big_key: row.Key,
            name: this.editName,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"修改成功！",
              offset:80
            });
            this.dialogVisible2 = false;
            this.getList();
          } else {
            this.$notify({
              title: "修改失败",
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
    subDel: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/deletetypesmall", {
          params: {
            key: row.Key,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"删除成功！",
              offset:80
            });
            this.dialogVisible = false;
            this.getList();
          } else {
            this.$notify({
              title: "删除失败",
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
    mainDel: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/deletetypebig", {
          params: {
            big_key: row.BigKey,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"删除成功！",
              offset:80
            });
            this.dialogVisible = false;
            this.getList();
          } else {
            this.$notify({
              title: "删除失败",
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
  },
};
</script>
<style scoped>
#item-list {
  margin: 0;
  margin-left: 250px;
}
</style>