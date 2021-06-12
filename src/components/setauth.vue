<template>
  <div id="set-auth">
    <p>搜索并选中用户以设置权限</p>
    <p>可通过姓名，学号/工号，openid和电话搜索</p>
    <el-input
      style="width: 300px"
      v-model="searchKey"
      placeholder="输入搜索"
    ></el-input>
    <el-button @click="search()">搜索</el-button>
    <el-table
      ref="singleTable"
      :data="tableData"
      highlight-current-row
      @current-change="handleCurrentChange"
      style="width: 100%"
    >
      <!-- <el-table-column type="index" width="50"> </el-table-column> -->
      <el-table-column property="OpenId" label="OpenId" width="300">
      </el-table-column>
      <el-table-column property="Name" label="姓名"> </el-table-column>
      <el-table-column property="UserId" label="学号/工号"></el-table-column>
      <el-table-column property="Mobile" label="电话"></el-table-column>
    </el-table>
    <p>选择权限</p>
    <el-select v-model="authVal" placeholder="请选择">
      <el-option
        v-for="item in authOp"
        :key="item.value"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
    <el-cascader
      placeholder="请选择地点"
      v-show="authVal == 1"
      v-model="placeVal"
      :options="placeList"
      :props="{ expandTrigger: 'hover' }"
      @change="handleChange"
    ></el-cascader>
    <p>
      <el-button @click="submit">确认</el-button>
    </p>
  </div>
</template>
<script>
export default {
  name: "setauth",
  mounted() {
    this.getPlaceList();
  },
  data() {
    return {
      searchKey: null,
      currentRow: null,
      authVal: null,
      placeVal: null,
      placeList: [],
      authOp: [
        {
          label: "超级管理员",
          value: "3",
        },
        {
          label: "平台审核管理员",
          value: "2",
        },
        {
          label: "地点管理员",
          value: "1",
        },
        {
          label: "普通用户",
          value: "0",
        },
      ],
      tableData: [],
    };
  },
  methods: {
    submit: function () {
      if(this.authVal==1){
        this.setPlaceAd();
      }else{
        this.setNormalAd();
      }
    },
    setNormalAd: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/setAdminPrivilage", {
          params: {
            open_id: this.currentRow.OpenId,
            privilage: this.authVal,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.$message({
              message: "设置成功！",
              offset: 80,
            });
          } else {
            this.$notify({
              title: "设置失败",
              message: res.data.msg,
              offset: 100,
            });
          }
        });
    },
    setPlaceAd:function(){
      this.$axios.get("https://www.fengzigeng.com/api/management/setPlaceAdmin",{
        params:{
          open_id:this.currentRow.OpenId,
          place_key:this.placeVal[2]
        }
      }).then((res)=>{
          if (res.data.code == 200) {
            this.$message({
              message: "设置成功！",
              offset: 80,
            });
          } else {
            this.$notify({
              title: "设置失败",
              message: res.data.msg,
              offset: 100,
            });
          }
      })
    },
    getPlaceList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/getPlaces")
        .then((res) => {
          if (res.data.code == 200) {
            this.placeList = res.data.data;
          } else {
            this.$notify({
              title: "获取地点失败",
              message: res.data.msg,
              offset: 100,
            });
          }
        });
    },
    search: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/searchUser", {
          params: {
            key: this.searchKey,
          },
        })
        .then((res) => {
          if (res.data.code == 200) {
            this.tableData = res.data.data;
          } else {
            this.$notify({
              title: "搜索失败",
              message: res.data.msg,
              offset: 100,
            });
          }
        });
    },
    handleChange(value) {
      console.log(value);
    },
    handleCurrentChange(val) {
      this.currentRow = val;
      console.log(this.currentRow);
    },
  },
};
</script>
<style scoped>
#set-auth {
  margin: 0;
  margin-left: 250px;
  padding-top: 12px;
}
</style>