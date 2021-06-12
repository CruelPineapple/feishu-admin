<template>
  <div id="auth">
    <div class="auth-list">
      <p style="margin-top:0px">管理员列表</p>
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
  mounted() {},
  data() {
    return {
      tableData: [
        {
          ID: 1,
          OpenId: "ou_273dbf68377bc685de3dd11c6102f879",
          Name: "冯梓耕",
          Avatar:
            "https://s1-fs.pstatp.com/static-resource/v1/2ed0efbc-72f8-45da-9c93-9c4468f2e2fg~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          Mobile: "+8613546519806",
          UserId: "2019091201002",
          Permission: "超级管理员",
          PlaceName: "",
        },
        {
          ID: 2,
          OpenId: "ou_4ca51d5d19af5f44898a8a0b5abfc683",
          Name: "李尚哲",
          Avatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          Mobile: "+8615976885032",
          UserId: "2019091601021",
          Permission: "超级管理员",
          PlaceName: "",
        },
      ],
    };
  },
  methods: {},
};
</script>
<style scoped>
#auth {
  margin: 0;
  margin-left: 250px;
  padding-top: 12px;
}
</style>