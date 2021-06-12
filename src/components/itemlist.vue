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
      tableData: [
        {
          BigName: "个人物品",
          SmallName: "衣物（含帽子手套围巾等）",
          Key: 39,
          BigKey: 5,
        },
        {
          BigName: "学习用品",
          SmallName: "笔袋",
          Key: 35,
          BigKey: 4,
        },
        {
          BigName: "电子设备",
          SmallName: "手机",
          Key: 1,
          BigKey: 1,
        },
        {
          BigName: "证件或证书",
          SmallName: "一卡通",
          Key: 15,
          BigKey: 2,
        },
        {
          BigName: "电子设备",
          SmallName: "平板电脑",
          Key: 2,
          BigKey: 1,
        },
        {
          BigName: "证件或证书",
          SmallName: "身份证",
          Key: 16,
          BigKey: 2,
        },
        {
          BigName: "个人物品",
          SmallName: "包",
          Key: 40,
          BigKey: 5,
        },
        {
          BigName: "学习用品",
          SmallName: "书籍",
          Key: 36,
          BigKey: 4,
        },
        {
          BigName: "学习用品",
          SmallName: "纸质笔记本",
          Key: 37,
          BigKey: 4,
        },
        {
          BigName: "电子设备",
          SmallName: "电纸书",
          Key: 3,
          BigKey: 1,
        },
        {
          BigName: "证件或证书",
          SmallName: "学生证",
          Key: 17,
          BigKey: 2,
        },
        {
          BigName: "个人物品",
          SmallName: "眼镜",
          Key: 41,
          BigKey: 5,
        },
        {
          BigName: "学习用品",
          SmallName: "其它学习物品",
          Key: 38,
          BigKey: 4,
        },
        {
          BigName: "电子设备",
          SmallName: "笔记本电脑",
          Key: 4,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "钱包",
          Key: 42,
          BigKey: 5,
        },
        {
          BigName: "证件或证书",
          SmallName: "健身卡",
          Key: 18,
          BigKey: 2,
        },
        {
          BigName: "电子设备",
          SmallName: "耳机",
          Key: 5,
          BigKey: 1,
        },
        {
          BigName: "证件或证书",
          SmallName: "考试通过证书",
          Key: 19,
          BigKey: 2,
        },
        {
          BigName: "个人物品",
          SmallName: "钥匙",
          Key: 43,
          BigKey: 5,
        },
        {
          BigName: "证件或证书",
          SmallName: "比赛奖状",
          Key: 20,
          BigKey: 2,
        },
        {
          BigName: "个人物品",
          SmallName: "水杯",
          Key: 44,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "充电器",
          Key: 6,
          BigKey: 1,
        },
        {
          BigName: "证件或证书",
          SmallName: "其他证件或证书",
          Key: 21,
          BigKey: 2,
        },
        {
          BigName: "电子设备",
          SmallName: "充电宝",
          Key: 7,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "化妆品",
          Key: 45,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "数据线",
          Key: 8,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "首饰",
          Key: 46,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "智能手表",
          Key: 9,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "笔袋",
          Key: 47,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "U盘",
          Key: 10,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "未领走快递",
          Key: 48,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "Apple Pencil",
          Key: 11,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "雨伞",
          Key: 49,
          BigKey: 5,
        },
        {
          BigName: "个人物品",
          SmallName: "运动器械相关",
          Key: 50,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "鼠标",
          Key: 12,
          BigKey: 1,
        },
        {
          BigName: "个人物品",
          SmallName: "其它个人物品",
          Key: 51,
          BigKey: 5,
        },
        {
          BigName: "电子设备",
          SmallName: "键盘",
          Key: 13,
          BigKey: 1,
        },
        {
          BigName: "电子设备",
          SmallName: "其他电子设备",
          Key: 14,
          BigKey: 1,
        },
      ],
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
            this.$message("修改成功！");
            this.dialogVisible2 = false;
            this.getList();
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
        .get("https://www.fengzigeng.com/api/management/edittypebig", {
          params: {
            big_key: row.Key,
            name: this.editName,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message("修改成功！");
            this.dialogVisible2 = false;
            this.getList();
          } else {
            this.$notify({
              title: "修改失败",
              message: res.data.msg,
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
            this.$message("删除成功！");
            this.dialogVisible = false;
            this.getList();
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
        .get("https://www.fengzigeng.com/api/management/deletetypebig", {
          params: {
            big_key: row.BigKey,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message("删除成功！");
            this.dialogVisible = false;
            this.getList();
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
#item-list {
  margin: 0;
  margin-left: 250px;
}
</style>