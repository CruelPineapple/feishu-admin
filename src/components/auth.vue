<template>
  <div id="auth">
    <div class="auth-list">
      <!-- <div class="title" style="margin-top:0px">
        <p>管理员列表</p>
        <el-button @click="getList()" class="btn">刷新</el-button>
      </div> -->
      <el-dialog
        :show-close="false"
        title="提示"
        :visible="dialogVisible2"
        width="60%"
      >
        <p>调整权限</p>

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

        <span slot="footer" class="dialog-footer">
          <el-button type="confirm" @click="confirm"
            >确认</el-button
          >
          <el-button @click="dialogVisible2 = false">取消</el-button>
        </span>
      </el-dialog>
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column
          prop="OpenId"
          label="OpenId"
          width="300"
        ></el-table-column>
        <el-table-column prop="UserId" label="学号/工号"> </el-table-column>
        <el-table-column prop="Name" label="姓名"></el-table-column>
        <el-table-column prop="Mobile" label="电话"> </el-table-column>
        <el-table-column prop="Permission" label="权限"> </el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
              >编辑</el-button
            >
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>
<script>
export default {
  name: "auth",
  mounted() {
    this.getList();
    this.getPlaceList();
  },
  data() {
    return {
      currentRow: null,
      placeList: [],
      placeVal: null,
      authVal: null,
      dialogVisible2: false,
      tableData: [],
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
    };
  },
  methods: {
    confirm: function () {
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
            this.dialogVisible2 = false;
            this.getList();
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
            this.dialogVisible2 = false;
            this.getList();
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
    handleEdit(index, row) {
      console.log(index, row);
      this.dialogVisible2 = true;
      this.currentRow = row;
    },
    getList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/getAdmins")
        .then((res) => {
          if (res.data.code == 200) {
            this.tableData = res.data.data;
          } else {
            this.$notify({
              title: "获取管理员失败",
              message: res.data.msg,
              offset: 100,
            });
          }
        });
    },
  },
};
</script>
<style scoped>
#auth {
  margin: 0;
  margin-left: 250px;
  padding-top: 12px;
}
.btn {
  position: absolute;
  right: 12px;
  top: 75px;
}
</style>