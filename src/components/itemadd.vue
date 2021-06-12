<template>
  <div id="item-add">
    <h3 style="margin-top: 0" class="title">新增物品</h3>
    <p class="normal">
      先选择一个大类物品，再填写物品名称。删除物品需前往物品类型列表
    </p>
    <el-select v-model="pickerValue" placeholder="请选择">
      <el-option
        v-for="item in pickerData"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
    <el-input
      style="width: 193px"
      v-model="subType"
      placeholder="物品名称"
    ></el-input>
    <el-button @click="confirmSub">确认</el-button>
    <h3 class="title">新建物品种类</h3>
    <p class="normal">删除物品种类需前往物品类型列表</p>
    <el-input
      style="width: 193px"
      v-model="mainType"
      placeholder="物品种类名称"
    ></el-input>
    <el-button @click="confirmMain">确认</el-button>
  </div>
</template>
<script>
export default {
  name: "itemadd",
  mounted() {
    this.getPicker();
  },
  data() {
    return {
      mainType: "",
      subType: "",
      pickerValue: undefined,
      pickerData: [],
    };
  },
  methods: {
    confirmMain: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/puttypebig", {
          params: {
            name: this.mainType,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"新建物品种类成功",
              offset:80
            });
            this.getPicker();
          } else {
            this.$notify({
              title: "新建物品种类失败",
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
    confirmSub: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/puttypesmall", {
          params: {
            big_key: this.pickerValue,
            name: this.subType,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"新建物品成功",
              offset:80
            });
            this.getPicker();
          } else {
            this.$notify({
              title: "新建物品失败",
              message: res.data.msg,
              duration: 5,
              offset: 100
            });
          }
        });
    },
    getPicker: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/typebig")
        .then((res) => {
          if (res.data.code == 200) {
            this.pickerData = res.data.data;
          } else {
            this.$notify({
              title: "获取物品类型失败",
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
#item-add {
  margin: 0;
  margin-left: 250px;
  padding-top: 20px;
}
.title {
  color: #303133;

}
.normal {
  color: #606266;
}
</style>