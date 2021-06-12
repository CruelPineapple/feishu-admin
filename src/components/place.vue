<template>
  <div id="place">
    <el-dialog
      :show-close="false"
      title="提示"
      :visible="dialogVisible"
      width="30%"
    >
      <span>请选择删除方式</span>
      <span slot="footer" class="dialog-footer">
        <el-button type="danger" @click="subDel(delBuff)">删除子地点</el-button>
        <el-button type="danger" @click="mainDel(delBuff)"
          >删除父地点</el-button
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
    <div class="school-picker">
      <el-radio @change="schoolRadioChange" v-model="radio" label="1"
        >沙河校区</el-radio
      >
      <el-radio @change="schoolRadioChange" v-model="radio" label="0"
        >清水河校区</el-radio
      >
    </div>
    <div class="table-container">
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column label="校区" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.Campus }}</span>
          </template>
        </el-table-column>
        <el-table-column label="大类地点" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.Place }}</span>
          </template>
        </el-table-column>
        <el-table-column label="地点" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.SubPlace }}</span>
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
  name: "place",
  mounted() {
    this.$axios
      .get("https://www.fengzigeng.com/api/management/place", {
        params: {
          campus_id: 1,
        },
      })
      .then((res) => {
        if (res.data.code == 200) {
          this.tableData = res.data.data;
        } else {
          this.$notify.error({
            title: "错误",
            dangerouslyUseHTMLString: true,
            message: `<a href= "https://www.fengzigeng.com/api/weblogin">点此重新登录</a>`,
          });
        }
      });
  },
  data() {
    return {
      radio: "1",
      editName: "",
      dialogVisible2: false,
      editBuff: undefined,
      dialogVisible: false,
      delBuff: undefined,
      tableData: [],
    };
  },
  methods: {
    subEdit: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/editplacesmall", {
          params: {
            key: row.Key,
            name: this.editName,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message("修改成功！");
            this.dialogVisible2 = false;
            this.schoolRadioChange();
          } else {
            this.$notify({
              title: "修改失败",
              message: res.data.msg,
            });
          }
        });
    },
    mainEdit: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/editplacebig", {
          params: {
            big_key: row.Key,
            name: this.editName,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message("修改成功！");
            this.dialogVisible2 = false;
            this.schoolRadioChange();
          } else {
            this.$notify({
              title: "修改失败",
              message: res.data.msg,
            });
          }
        });
    },
    schoolRadioChange: function () {
      console.log(this.radio);
      this.$axios
        .get("https://www.fengzigeng.com/api/management/place", {
          params: {
            campus_id: this.radio,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.tableData = res.data.data;
          } else {
            this.$notify.error({
              title: "错误",
              dangerouslyUseHTMLString: true,
              message: `<a href= "https://www.fengzigeng.com/api/weblogin">点此重新登录</a>`,
            });
          }
        });
    },
    handleEdit(index, row) {
      console.log(index, row);
      this.dialogVisible2 = true;
      this.editBuff = row;
    },
    handleDelete(index, row) {
      console.log(index, row);
      this.dialogVisible = true;
      this.delBuff = row;
    },
    subDel: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/deletesubplace", {
          params: {
            key: row.Key,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message("删除成功！");
            this.dialogVisible = false;
            this.schoolRadioChange();
          } else {
            this.$notify({
              title: "删除失败",
              message: res.data.msg,
            });
          }
        });
    },
    mainDel: function (row) {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/deleteplace", {
          params: {
            big_key: row.BigKey,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message("删除成功！");
            this.dialogVisible = false;
            this.schoolRadioChange();
          } else {
            this.$notify({
              title: "删除失败",
              message: res.data.msg,
            });
          }
        });
    },
  },
};
</script>

<style scoped>
#place {
  margin: 0;
  margin-left: 250px;
}
.table-container {
  padding-top: 20px;
}
.school-picker {
  text-align: left;
  padding-top: 20px;
  margin-bottom: 20px;
  margin-left: 250px;
}
</style>
