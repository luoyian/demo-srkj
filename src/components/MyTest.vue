<template>
  <div class="my-test">
    <div class="box">
      <div class="shadow"></div>
      <div class="boxxx">
        <el-progress class="Elprogress" type="circle" :percentage="value" :width="200" :show-text="false"
        :stroke-width="30">
      </el-progress>
      </div>
      <div class="textCenter">
        <div class="text-value">{{ value }}%</div>
        <span>异常分数</span>
      </div>
      <!-- svg -->
      <div class="svg-box">
        <svg width="100%" height="100%">
          <defs>
            <linearGradient id="purple" x1="100%" y1="0%" x2="0%" y2="100%">
              <stop offset="0%" style="stop-color: #9373f0" stop-opacity="1"></stop>
              <stop offset="100%" style="stop-color: rgb(213, 201, 244)" stop-opacity="1"></stop>
            </linearGradient>
          </defs>
        </svg>
      </div>
      <!-- 检测状态 -->
      <div class="img">
        <img :src="imgSrc" alt="" />
        <div class="text">
          <span class="title">检测状态</span>
          <span ref="active" style="font-weight: 600; color: #999;">{{ textValue }}</span>
        </div>
      </div>
    </div>
    <!-- 滑块 -->
    <div class="block">
      <el-slider v-model="value"></el-slider>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: 0,
      imgSrc: require('../assets/weizhi@3x.png'),
      textValue: '未知'
    }
  },
  watch: {
    value: {
      handler(val) {
        if (val === 0) {
          this.imgSrc = require('../assets/weizhi@3x.png')
          this.textValue = '未知'
          this.$refs.active.style.color = '#999'
        } else if (val > 0 && val <= 50) {
          this.imgSrc = require('../assets/zhengchang@3x.png')
          this.textValue = '正常'
          this.$refs.active.style.color = '#80c6fa'
        } else {
          this.imgSrc = require('../assets/baojing@3x.png')
          this.textValue = '报警'
          this.$refs.active.style.color = '#eb5353'
        }
      },
    },
  },
}
</script>

<style  lang="scss">
 .boxxx {

  // 进度条颜色
  svg>path:nth-child(2) {
    stroke: url(#purple);
  }
}

.shadow {
  height: 200px;
  width: 200px;
  border-radius: 50%;
  background-color: rgb(221, 220, 237);
  transform: translateY(2px);
  z-index: -2;
  position: absolute;

}

.shadow::after {
  position: absolute;
  content: '';
  background: white;
  height: 100px;
  width: 100px;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
  transform: scale(1.375);
  border-radius: 50%;
  z-index: -1;

}

.my-test {
  margin-top: 100px;
  text-align: center;
}

.box {

  display: flex;
  flex-direction: column;
  align-items: center;
}

.img {
  display: flex;
  justify-content: start;
  align-items: center;
  margin-top: 20px;
}

.img img {
  width: 50px;
  height: 50px;
}

.text {
  display: flex;
  flex-direction: column;
  align-items: start;
  margin-left: 10px;
  font-size: 14px;

  .title {
    color: #ccc;
  }
}

.block {
  width: 800px;
  margin: 0 auto;
}

.box {
  position: relative;
  margin: 40px 0;
}

.textCenter {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -230%);
}

.text-value {
  font-size: 30px;
  color: #9373f0;
}
</style>
