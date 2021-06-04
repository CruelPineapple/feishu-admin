<template>
  <div id="app">
    <div class="menu-container">
      <el-menu
        default-active="2"
        class="el-menu-vertical-demo"
        @select="handleSelect"
        @open="handleOpen"
        @close="handleClose"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#ffd04b"
      >
        <el-submenu index="1">
          <template slot="title">
            <i class="el-icon-location"></i>
            <span>物品列表</span>
          </template>
          <el-menu-item-group>
            <!-- <template slot="title">分组一</template> -->
            <el-menu-item index="1-1">失物列表</el-menu-item>
            <el-menu-item index="1-2">招领列表</el-menu-item>
            <el-menu-item index="1-3">已认领列表</el-menu-item>
          </el-menu-item-group>
          <!-- <el-submenu index="1-4">
            <template slot="title">选项4</template>
            <el-menu-item index="1-4-1">选项1</el-menu-item>
          </el-submenu> -->
        </el-submenu>
        <el-menu-item index="2">
          <i class="el-icon-menu"></i>
          <span slot="title">地点管理</span>
        </el-menu-item>
        <el-menu-item index="3">
          <i class="el-icon-document"></i>
          <span slot="title">人员管理</span>
        </el-menu-item>
        <el-menu-item index="4">
          <i class="el-icon-setting"></i>
          <span slot="title">导航四</span>
        </el-menu-item>
      </el-menu>
    </div>
    <place v-show="currentShow == 2"></place>
    <found v-show="currentShow == '1-2'"></found>
  </div>
</template>

<script>
import place from "./components/place";
import found from "./components/found";

export default {
  mounted() {
    // console.log(this.data[0].Campus);
    // this.transferPlace(this.data);
  },
  name: "App",
  components: { place, found },
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
      currentShow: 2,
    };
  },
  methods: {
    // transferPlace: function (data) {
    //   // let options=[];
    //   let lastVal1 = undefined;
    //   let lastVal2 = undefined;
    //   let lastVal3 = undefined;
    //   let val1Arr = [];
    //   let val2Arr = [];
    //   let val3Arr = [];
    //   data.forEach((element) => {
    //     let value1 = element.Key[0];
    //     if (value1 != lastVal1) {
    //       val1Arr.push(value1);
    //       lastVal1 = value1;
    //     }
    //     let value2 = element.Key[1];
    //     if (value2 != lastVal2) {
    //       val2Arr.push(value2);
    //       lastVal2 = value2;
    //     }
    //     let value3 = element.Key[2];
    //     if (value3 != lastVal3) {
    //       val3Arr.push(value3);
    //       lastVal3 = value3;
    //     }
    //     // let label1=element.Campus;
    //     // let label2=element.Place;
    //     // let label3=element.SubPlace;
    //   });
    //   let pos0 = [];
    //   let idx = val3Arr.indexOf(0);
    //   while (idx != -1) {
    //     pos0.push(idx);
    //     idx = val3Arr.indexOf(0, idx + 1);
    //   }
    //   let obj = {};
    //   for (let i = 0; i < pos0.length; i++) {
    //     obj["arr" + i] = val3Arr.slice(pos0[i], pos0[i + 1]);
    //   }

    //   let totalCnt=0;
    //   for(let i=0;i<Object.keys(obj).length;i++){
    //     for(let j=0;j<obj["arr"+i].length;j++){

    //     }
    //   }

    //   console.log(val1Arr);
    //   console.log(val2Arr);
    //   console.log(val3Arr);
    //   console.log("pos0", pos0);
    //   console.log("obj", obj);
    // },
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
      this.currentShow = key;
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
html {
  height: 100%;
}
body {
  margin: 0;
  height: 100%;
}

.el-menu-vertical-demo {
  border-right: none;
  height: 100%;
}
.menu-container {
  position: fixed;
  width: 250px;
  height: 100%;
  background-color: rgb(84, 92, 100);
}
</style>
