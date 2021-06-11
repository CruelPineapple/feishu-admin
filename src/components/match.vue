<template>
  <div class="match">
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column type="expand">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="失主学号/工号">
              <span>{{ props.row.LosterId }}</span>
            </el-form-item>
            <el-form-item label="拾到者学号/工号">
              <span>{{ props.row.FounderId }}</span>
            </el-form-item>
            <el-form-item label="失主手机号">
              <span>{{ props.row.LosterMoblie }}</span>
            </el-form-item>
            <el-form-item label="拾到者手机号">
              <span>{{ props.row.FounderMoblie }}</span>
            </el-form-item>
            <el-form-item label="拾到时间">
              <span>{{ props.row.FoundDate }} {{ props.row.FoundTime }}</span>
            </el-form-item>
            <el-form-item label="补充信息">
              <span>{{ props.row.AdditionalInfo }}</span>
            </el-form-item>
            <el-form-item label="感谢留言">
              <span>{{ props.row.ThxMsg }}</span>
            </el-form-item>
            <el-form-item label="图片">
              <el-image
                style="width: 150px; height: 150px"
                fit="cover"
                :src="props.row.Image"
              ></el-image>
            </el-form-item>
          </el-form>
        </template>
      </el-table-column>
      <el-table-column label="失物类型" prop="ItemType"> </el-table-column>
      <el-table-column label="失物信息" prop="Info"> </el-table-column>
      <el-table-column label="失主姓名" prop="LosterName"> </el-table-column>
      <el-table-column label="拾到者姓名" prop="FounderName"> </el-table-column>
      <el-table-column label="拾到日期" prop="FoundDate"> </el-table-column>
      <el-table-column label="地点" prop="Place"> </el-table-column>
      <el-table-column label="详细地点" prop="PlaceDetail"> </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <!-- <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button> -->
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
</template>
<script>
export default {
  name: "match",
  mounted() {
    this.getList();
  },
  methods: {
    getList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/match", {})
        .then((res) => {
          if (res.data.code == 200) {
            this.tableData = res.data.data;
          } else {
            this.$notify.error({
              title: "错误" + res.data.code,
              message: res.data.msg,
            });
          }
        });
    },
    handleEdit(index, row) {
      console.log(index, row);
    },
    handleDelete(index, row) {
      console.log(index, row);
    },
  },
  data() {
    return {
      tableData: [
        {
          FoundID: 1,
          FounderName: "邓雯月",
          FounderId: "2019091620026",
          FounderMoblie: "+8618843420822",
          FounderAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/258f7d52-0a2a-4225-ae94-8a0de663b46g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          LosterName: "李尚哲",
          LosterId: "2019091601021",
          LosterMoblie: "+8615976885032",
          LosterAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          ItemType: "电子设备-耳机",
          Info: "蓝牙耳机",
          AdditionalInfo: "",
          Campus: "沙河校区",
          Place: "宿舍区",
          PlaceDetail: "一楼大厅",
          Image:
            "https://www.fengzigeng.com/api/image?name=f08aaff79009d10ca7c01ee12bccec28.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:08",
          ThxMsg: "测试中! 十分感谢",
        },
        {
          FoundID: 2,
          FounderName: "邓雯月",
          FounderId: "2019091620026",
          FounderMoblie: "+8618843420822",
          FounderAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/258f7d52-0a2a-4225-ae94-8a0de663b46g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          LosterName: "李尚哲",
          LosterId: "2019091601021",
          LosterMoblie: "+8615976885032",
          LosterAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          ItemType: "证件或证书-一卡通",
          Info: "一卡通",
          AdditionalInfo: "",
          Campus: "沙河校区",
          Place: "宿舍区",
          PlaceDetail: "一楼水房",
          Image:
            "https://www.fengzigeng.com/api/image?name=71651ba32d2d4883af391bf9d67d3877.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:09",
          ThxMsg: "测试中! 谢谢",
        },
        {
          FoundID: 3,
          FounderName: "邓雯月",
          FounderId: "2019091620026",
          FounderMoblie: "+8618843420822",
          FounderAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/258f7d52-0a2a-4225-ae94-8a0de663b46g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          LosterName: "李尚哲",
          LosterId: "2019091601021",
          LosterMoblie: "+8615976885032",
          LosterAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          ItemType: "电子设备-耳机",
          Info: "有线耳机",
          AdditionalInfo: "",
          Campus: "沙河校区",
          Place: "教学楼",
          PlaceDetail: "203教室",
          Image:
            "https://www.fengzigeng.com/api/image?name=9d84e52f22071966703387c441ddbb82.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:12",
          ThxMsg: "为什么show toast不显示？",
        },
        {
          FoundID: 5,
          FounderName: "冯梓耕",
          FounderId: "2019091201002",
          FounderMoblie: "+8613546519806",
          FounderAvatar:
            "https://s3-fs.pstatp.com/static-resource/v1/2ed0efbc-72f8-45da-9c93-9c4468f2e2fg~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          LosterName: "邓雯月",
          LosterId: "2019091620026",
          LosterMoblie: "+8618843420822",
          LosterAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/258f7d52-0a2a-4225-ae94-8a0de663b46g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          ItemType: "电子设备-耳机",
          Info: "AirPods",
          AdditionalInfo: "",
          Campus: "沙河校区",
          Place: "教学楼",
          PlaceDetail: "二教103第一排",
          Image:
            "https://www.fengzigeng.com/api/image?name=819cdb77f8fde8bc72b882f13efd21ee.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:17",
          ThxMsg: "谢谢您～",
        },
        {
          FoundID: 6,
          FounderName: "冯梓耕",
          FounderId: "2019091201002",
          FounderMoblie: "+8613546519806",
          FounderAvatar:
            "https://s3-fs.pstatp.com/static-resource/v1/2ed0efbc-72f8-45da-9c93-9c4468f2e2fg~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          LosterName: "邓雯月",
          LosterId: "2019091620026",
          LosterMoblie: "+8618843420822",
          LosterAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/258f7d52-0a2a-4225-ae94-8a0de663b46g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          ItemType: "个人物品-雨伞",
          Info: "黑色雨伞",
          AdditionalInfo: "",
          Campus: "沙河校区",
          Place: "教学楼",
          PlaceDetail: "门口台阶",
          Image:
            "https://www.fengzigeng.com/api/image?name=c365e5b63bd21fe253c7d2d4f32b0ce6.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:24",
          ThxMsg: "谢谢～",
        },
        {
          FoundID: 7,
          FounderName: "冯梓耕",
          FounderId: "2019091201002",
          FounderMoblie: "+8613546519806",
          FounderAvatar:
            "https://s3-fs.pstatp.com/static-resource/v1/2ed0efbc-72f8-45da-9c93-9c4468f2e2fg~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          LosterName: "邓雯月",
          LosterId: "2019091620026",
          LosterMoblie: "+8618843420822",
          LosterAvatar:
            "https://s1-fs.pstatp.com/static-resource/v1/258f7d52-0a2a-4225-ae94-8a0de663b46g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          ItemType: "证件或证书-一卡通",
          Info: "绿色硕士一卡通",
          AdditionalInfo: "请通过飞书与我联系",
          Campus: "沙河校区",
          Place: "食堂",
          PlaceDetail: "柜台处发现",
          Image:
            "https://www.fengzigeng.com/api/image?name=0f18aa14d40e0787d4eda0a477a0d373.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:29",
          ThxMsg: "谢谢～",
        },
      ],
    };
  },
};
</script>
<style scoped>
.match {
  margin: 0;
  margin-left: 250px;
}
.demo-table-expand {
  font-size: 0;
}
.demo-table-expand label {
  width: 90px;
  color: #99a9bf;
}
.demo-table-expand .el-form-item {
  margin-right: 0;
  margin-bottom: 0;
  width: 50%;
}
</style>
