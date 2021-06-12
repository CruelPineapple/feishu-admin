<template>
  <div id="auth">
    <div class="auth-list">
      <!-- <div class="title" style="margin-top:0px">
        <p>管理员列表</p>
        <el-button @click="getList()" class="btn">刷新</el-button>
      </div> -->
      
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column prop="OpenId" label="OpenId" width="300"></el-table-column>
        <el-table-column prop="UserId" label="学号/工号" > </el-table-column>
        <el-table-column prop="Name" label="姓名" ></el-table-column>
        <el-table-column prop="Mobile" label="电话" > </el-table-column>
        <el-table-column prop="Permission" label="权限" > </el-table-column>
      </el-table>
    </div>
  </div>
</template>
<script>
export default {
  name: "auth",
  mounted() {
    this.getList();
  },
  data() {
    return {
      tableData: [],
    };
  },
  methods: {
      getList:function(){
        this.$axios.get("https://www.fengzigeng.com/api/management/getAdmins").then((res)=>{
          if(res.data.code==200){
            this.tableData=res.data.data;
          }else{
            this.$notify({
              title: "获取管理员失败",
              message: res.data.msg,
              offset: 100
            });
          }
        })
      }
  },
};
</script>
<style scoped>
#auth {
  margin: 0;
  margin-left: 250px;
  padding-top: 12px;
}
.btn{
  position: absolute;
  right: 12px;
  top :75px;
}
</style>