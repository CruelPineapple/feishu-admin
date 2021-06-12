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
    <p>先选择父地点所属校区，再填写父地点名称</p>
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
      pickerData: [
        {
          value: "0",
          label: "清水河校区",
          children: [
            {
              label: "教学楼",
              value: 1,
            },
            {
              label: "硕丰苑",
              value: 2,
            },
            {
              label: "学知苑",
              value: 3,
            },
            {
              label: "博翰苑",
              value: 4,
            },
            {
              label: "留学生宿舍区",
              value: 5,
            },
            {
              label: "餐厅",
              value: 6,
            },
            {
              label: "其他",
              value: 7,
            },
          ],
        },
        {
          value: "1",
          label: "沙河校区",
          children: [
            {
              label: "教学楼",
              value: 8,
            },
            {
              label: "宿舍区",
              value: 9,
            },
            {
              label: "食堂",
              value: 10,
            },
            {
              label: "运动场所",
              value: 11,
            },
            {
              label: "其它",
              value: 12,
            },
            {
              label: "测试特殊特森的天涯翠凤",
              value: 15,
            },
          ],
        },
      ],
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
            this.$message("新建地址成功");
            this.getPicker();
          } else {
            this.$notify({
              title: "新建地址失败",
              message: res.data.msg,
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
            this.$message("新建地址成功");
            this.getPicker();
          } else {
            this.$notify({
              title: "新建地址失败",
              message: res.data.msg,
              duration: 5,
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
}
.title {
  color: #303133;

}
.normal {
  color: #606266;
}
</style>