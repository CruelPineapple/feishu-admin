<template>
  <div class="found">
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column type="expand">
        <template slot-scope="props">
          <el-form label-position="left" inline class="demo-table-expand">
            <el-form-item label="学号/工号">
              <span>{{ props.row.Student_Teacher_Id }}</span>
            </el-form-item>
            <el-form-item label="手机号">
              <span>{{ props.row.Moblie }}</span>
            </el-form-item>
            <el-form-item label="拾到时间">
              <span>{{ props.row.FoundDate }} {{ props.row.FoundTime }}</span>
            </el-form-item>
            <el-form-item label="补充信息">
              <span>{{ props.row.AdditionalInfo }}</span>
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
      <el-table-column label="物品类型" prop="SubType"> </el-table-column>
      <el-table-column label="描述信息" prop="Info"> </el-table-column>
      <el-table-column label="拾到者" prop="Name"> </el-table-column>
      <el-table-column label="拾到日期" prop="FoundDate"> </el-table-column>
      <el-table-column label="校区" prop="Campus"> </el-table-column>
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
  name: "found",
  mounted(){
    this.getList();
  },
  methods: {
    getList: function () {
      this.$axios
        .get("https://www.fengzigeng.com/api/management/found", {

        })
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
          ID: 4,
          Validity: true,
          SubType: "雨伞",
          Name: "冯梓耕",
          Student_Teacher_Id: "2019091201002",
          Moblie: "+8613546519806",
          Avatar:
            "https://s3-fs.pstatp.com/static-resource/v1/2ed0efbc-72f8-45da-9c93-9c4468f2e2fg~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          Campus: "清水河校区",
          Place: "教学楼-品学楼A区",
          PlaceDetail: "品a101中间第四排",
          Image:
            "https://www.fengzigeng.com/api/image?name=b7ead0b3638441a7388ffb69d59d1984.jpg",
          ImageList:
            "https://www.fengzigeng.com/api/image?name=b7ead0b3638441a7388ffb69d59d1984.jpg",
          FoundDate: "2021-05-20",
          FoundTime: "21:12",
          Info: "一把天堂伞",
          AdditionalInfo: "",
        },
        {
          ID: 8,
          Validity: true,
          SubType: "手机",
          Name: "李尚哲",
          Student_Teacher_Id: "2019091601021",
          Moblie: "+8615976885032",
          Avatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          Campus: "沙河校区",
          Place: "运动场所-体育馆",
          PlaceDetail: "测试地点",
          Image:
            "https://www.fengzigeng.com/api/image?name=5649cc3937fc2e56b2f28ed9887de9cd.jpg",
          ImageList:
            "https://www.fengzigeng.com/api/image?name=5649cc3937fc2e56b2f28ed9887de9cd.jpg",
          FoundDate: "2021-06-06",
          FoundTime: "16:34",
          Info: "测试手机",
          AdditionalInfo: "没啥补充的",
        },
        {
          ID: 9,
          Validity: true,
          SubType: "耳机",
          Name: "李尚哲",
          Student_Teacher_Id: "2019091601021",
          Moblie: "+8615976885032",
          Avatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          Campus: "沙河校区",
          Place: "食堂-阳光餐厅",
          PlaceDetail: "测试地点",
          Image:
            "https://www.fengzigeng.com/api/image?name=c00dadb1064e7c853f2a41279b8cf9fa.jpg",
          ImageList:
            "https://www.fengzigeng.com/api/image?name=c00dadb1064e7c853f2a41279b8cf9fa.jpg",
          FoundDate: "2021-06-06",
          FoundTime: "16:38",
          Info: "测试耳机",
          AdditionalInfo: "",
        },
        {
          ID: 10,
          Validity: true,
          SubType: "笔袋",
          Name: "李尚哲",
          Student_Teacher_Id: "2019091601021",
          Moblie: "+8615976885032",
          Avatar:
            "https://s1-fs.pstatp.com/static-resource/v1/32503907-02d1-40d0-9d45-b179c66f9c3g~?image_size=72x72&cut_type=&quality=&format=image&sticker_format=.webp",
          Campus: "沙河校区",
          Place: "其它-图书馆",
          PlaceDetail: "桌子上",
          Image:
            "https://www.fengzigeng.com/api/image?name=5212674c95eacc7b80f7c698c6cadb02.jpg",
          ImageList:
            "https://www.fengzigeng.com/api/image?name=5212674c95eacc7b80f7c698c6cadb02.jpg",
          FoundDate: "2021-06-06",
          FoundTime: "16:39",
          Info: "测试笔袋",
          AdditionalInfo: "",
        },
      ],
    };
  },
};
</script>
<style scoped>
.found {
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
