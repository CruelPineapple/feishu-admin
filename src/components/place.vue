<template>
  <div id="place">
    <div class="school-picker">
      <el-radio @change="schoolRadioChange" v-model="radio" label="1"
        >沙河校区</el-radio
      >
      <el-radio @change="schoolRadioChange" v-model="radio" label="0"
        >清水河校区</el-radio
      >
    </div>
    <div class="table-container">
      <el-table :data="tableData" style="width: 100%">
        <el-table-column label="校区" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.Campus }}</span>
          </template>
        </el-table-column>
        <el-table-column label="大类地点" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.Place }}</span>
          </template>
        </el-table-column>
        <el-table-column label="地点" width="300">
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row.SubPlace }}</span>
          </template>
        </el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <!-- <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
              >编辑</el-button
            > -->
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
  name: "place",
  mounted() {
    this.$axios
      .get("https://www.fengzigeng.com/api/management/place", {
        params: {
          campus_id: 1,
        },
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
  data() {
    return {
      radio: "1",
      tableData: [
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "研究院大楼",
          Key: [0, 0, 0],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "四号科研楼A区",
          Key: [0, 0, 1],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "四号科研楼B区",
          Key: [0, 0, 2],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "四号科研楼C区",
          Key: [0, 0, 3],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "五号科研楼",
          Key: [0, 0, 4],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "综合楼",
          Key: [0, 0, 5],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "磁共振脑成像中心",
          Key: [0, 0, 6],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "科研楼",
          Key: [0, 0, 7],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "基础实验楼",
          Key: [0, 0, 8],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "品学楼A区",
          Key: [0, 0, 9],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "品学楼B区",
          Key: [0, 0, 10],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "品学楼C区",
          Key: [0, 0, 11],
        },
        {
          Campus: "清水河校区",
          Place: "教学楼",
          SubPlace: "立人楼",
          Key: [0, 0, 12],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑1栋",
          Key: [0, 1, 0],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑2栋",
          Key: [0, 1, 1],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑3栋",
          Key: [0, 1, 2],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑4栋",
          Key: [0, 1, 3],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑5栋",
          Key: [0, 1, 4],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑6栋",
          Key: [0, 1, 5],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑7栋",
          Key: [0, 1, 6],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑8栋",
          Key: [0, 1, 7],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑9栋",
          Key: [0, 1, 8],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑10栋",
          Key: [0, 1, 9],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑11栋",
          Key: [0, 1, 10],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑12栋",
          Key: [0, 1, 11],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑13栋",
          Key: [0, 1, 12],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑14栋",
          Key: [0, 1, 13],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑15栋",
          Key: [0, 1, 14],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑16栋",
          Key: [0, 1, 15],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑17栋",
          Key: [0, 1, 16],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑18栋",
          Key: [0, 1, 17],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑19栋",
          Key: [0, 1, 18],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑20栋",
          Key: [0, 1, 19],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑21栋",
          Key: [0, 1, 20],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑22栋",
          Key: [0, 1, 21],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑23栋",
          Key: [0, 1, 22],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑24栋",
          Key: [0, 1, 23],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑25栋",
          Key: [0, 1, 24],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑26栋",
          Key: [0, 1, 25],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑27栋",
          Key: [0, 1, 26],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "硕丰苑28栋",
          Key: [0, 1, 27],
        },
        {
          Campus: "清水河校区",
          Place: "硕丰苑",
          SubPlace: "hahahah",
          Key: [0, 1, 28],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑1栋",
          Key: [0, 2, 0],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑2栋",
          Key: [0, 2, 1],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑3栋",
          Key: [0, 2, 2],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑4栋",
          Key: [0, 2, 3],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑5栋",
          Key: [0, 2, 4],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑6栋",
          Key: [0, 2, 5],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑7栋",
          Key: [0, 2, 6],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑8栋",
          Key: [0, 2, 7],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑9栋",
          Key: [0, 2, 8],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑10栋",
          Key: [0, 2, 9],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑11栋",
          Key: [0, 2, 10],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑12栋",
          Key: [0, 2, 11],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑13栋",
          Key: [0, 2, 12],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑14栋",
          Key: [0, 2, 13],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑15栋",
          Key: [0, 2, 14],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑16栋",
          Key: [0, 2, 15],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑17栋",
          Key: [0, 2, 16],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑18栋",
          Key: [0, 2, 17],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑19栋",
          Key: [0, 2, 18],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑20栋",
          Key: [0, 2, 19],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑21栋",
          Key: [0, 2, 20],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑22栋",
          Key: [0, 2, 21],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑23栋",
          Key: [0, 2, 22],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑24栋",
          Key: [0, 2, 23],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑25栋",
          Key: [0, 2, 24],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑26栋",
          Key: [0, 2, 25],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑27栋",
          Key: [0, 2, 26],
        },
        {
          Campus: "清水河校区",
          Place: "学知苑",
          SubPlace: "学知苑28栋",
          Key: [0, 2, 27],
        },
        {
          Campus: "清水河校区",
          Place: "留学生宿舍区",
          SubPlace: "留学生2栋",
          Key: [0, 4, 0],
        },
        {
          Campus: "清水河校区",
          Place: "留学生宿舍区",
          SubPlace: "留学生3栋",
          Key: [0, 4, 1],
        },
        {
          Campus: "清水河校区",
          Place: "留学生宿舍区",
          SubPlace: "留学生4栋",
          Key: [0, 4, 2],
        },
        {
          Campus: "清水河校区",
          Place: "餐厅",
          SubPlace: "清真餐厅",
          Key: [0, 5, 0],
        },
        {
          Campus: "清水河校区",
          Place: "餐厅",
          SubPlace: "学生二食堂",
          Key: [0, 5, 1],
        },
        {
          Campus: "清水河校区",
          Place: "餐厅",
          SubPlace: "春晖苑（三食堂）",
          Key: [0, 5, 2],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "体育馆",
          Key: [0, 6, 0],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "游泳馆",
          Key: [0, 6, 1],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "体育场",
          Key: [0, 6, 2],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "众创空间",
          Key: [0, 6, 3],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼A1区",
          Key: [0, 6, 4],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼A2区",
          Key: [0, 6, 5],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼B1区",
          Key: [0, 6, 6],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼B2区",
          Key: [0, 6, 7],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼B3区",
          Key: [0, 6, 8],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼C2区",
          Key: [0, 6, 9],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "主楼C1区",
          Key: [0, 6, 10],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "图书馆",
          Key: [0, 6, 11],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "校医院",
          Key: [0, 6, 12],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "学生活动中心",
          Key: [0, 6, 13],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "成电会堂",
          Key: [0, 6, 14],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "商业街",
          Key: [0, 6, 15],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "综合训练馆",
          Key: [0, 6, 16],
        },
        {
          Campus: "清水河校区",
          Place: "其他",
          SubPlace: "游泳中心",
          Key: [0, 6, 17],
        },
      ],
    };
  },
  methods: {
    schoolRadioChange: function () {
      console.log(this.radio);
      this.$axios
        .get("https://www.fengzigeng.com/api/management/place", {
          params: {
            campus_id: this.radio,
          },
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
};
</script>

<style scoped>
#place {
  margin: 0;
  margin-left: 250px;
}
.table-container {
  padding-top: 20px;
}
.school-picker {
  text-align: left;
  padding-top: 20px;
  margin-bottom: 20px;
  margin-left: 250px;
}
</style>
