<template>
  <div id="edit">
    <h3 style="margin-top:0" class="title">新增子地点</h3>
    <p class="normal">先选择一个父地点，再填写子地点名称。删除子地点需前往地点列表</p>
    <el-cascader
      v-model="pickerValue"
      :options="pickerData"
      :props="{ expandTrigger: 'hover' }"
      @change="handleChange"
    ></el-cascader>
    <el-input
      style="width: 193px"
      v-model="subPlace"
      placeholder="子地点名称"
    ></el-input>
    <el-button @click="confirmSub">确认</el-button>
    <h3 class="title">新建父地点</h3>
    <p class="normal">先选择父地点所属校区，再填写父地点名称。删除父地点需前往地点列表</p>
    <div style="margin-bottom:8px" class="school-picker">
      <el-radio v-model="radio" label="1">沙河校区</el-radio>
      <el-radio v-model="radio" label="0">清水河校区</el-radio>
    </div>
    <el-input
      style="width: 193px"
      v-model="mainPlace"
      placeholder="父地点名称"
    ></el-input>
    <el-button @click="confirmMain">确认</el-button>
  </div>
</template>
<script>
export default {
  name: "edit",
  mounted() {
    this.$axios
      .get("https://www.fengzigeng.com/api/management/bigplace")
      .then((res) => {
        if (res.data.code == 200) {
          this.pickerData = res.data.data;
        } else {
          this.$notify({
            title: "错误",
            message: "获取父地点失败",
            duration: 5,
            offset: 100
          });
        }
      });
  },
  data() {
    return {
      radio: "1",
      mainPlace: "",
      subPlace: "",
      pickerValue: [],
      subPlaceKey: {},
      pickerData: [],
    };
  },
  methods: {
    getPicker:function(){
    this.$axios
      .get("https://www.fengzigeng.com/api/management/bigplace")
      .then((res) => {
        if (res.data.code == 200) {
          this.pickerData = res.data.data;
        } else {
          this.$notify({
            title: "错误",
            message: "获取父地点失败",
            duration: 5,
            offset: 100
          });
        }
      });
    },
    handleChange(value) {
      console.log(value[1]);
      this.subPlaceKey = value[1];
    },
    confirmMain: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/putplace", {
          params: {
            campus_id: this.radio,
            name: this.mainPlace,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"新建地址成功",
              offset:80
            });
            this.getPicker();
          } else {
            this.$notify({
              title: "新建地址失败",
              message: res.data.msg,
              offset: 100
            });
          }
        });
    },
    confirmSub: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/putsubplace", {
          params: {
            big_key: this.subPlaceKey,
            name: this.subPlace,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message:"新建地址成功",
              offset:80
            });
            this.getPicker();
          } else {
            this.$notify({
              title: "新建地址失败",
              message: res.data.msg,
              duration: 5,
              offset: 100
            });
          }
        });
    },
  },
};
</script>
<style scoped>
#edit {
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