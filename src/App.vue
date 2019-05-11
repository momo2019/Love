<template>
  <div style="position: relative; height: 100vh; width: 100vw;">
    <div v-if="pc">
      <div class="background">
        <Background :callback="showBook"/>
      </div>
      <div class="book" :style="display">
        <div class="tip">
          <Tip />
        </div>
        <Page
          v-for="(item, index) in data"
          :key="item.font.index + '-' + item.back.index"
          :isFirst="index === 0"
          :index="index"
          :sum="data.length"
          :font="item.font"
          :back="item.back"/>
      </div>
    </div>
    <div v-else>
      {{ '使用电脑打开,扣扣你了,窗口拉宽拉高点,全屏按F11。' }}
    </div>
    <audio src="assets/music/music.mp3" controls autoplay loop hidden="true"></audio>
  </div>
</template>

<script>
import Page from './components/Page.vue'
import Background from './components/Background.vue'
import Tip from './components/Tip.vue'

export default {
  name: 'app',
  components: {
    Page,
    Background,
    Tip
  },
  data () {
    return {
      data: [{
        font: {
          title: '很高心遇见你',
          img: 'assets/fm.jpg'
        },
        back: {
          img: 'assets/back1.jpg'
        }
      },{
        font: {
          title: '我想给你写一封情书',
          content: '我想给你写一封情书_在阳光灿烂的午后_在长满爬山虎的窗前_在风灌满两袖的麦田_在橘子味汽水的夏天_提笔却不知从何记起',
          index: '001',
          img: 'assets/page1.png'
        },
        back: {
          img: 'assets/back2.png'
        }
      },{
        font: {
          title: '山水一程 三生有幸',
          content: '我很想要过这样一个温暖的冬天_有一场踩起来嘎吱嘎吱的大雪_有路灯下昏黄得模糊的暖光_有热烘烘的烤地瓜_有一壶暖胃的酒有本想看的书_有窗上的雾有大毛毯_还有你一房~两人~三餐~四季',
          index: '002',
          img: 'assets/page2.jpg'
        },
        back: {
          img: 'assets/back3.jpg'
        }
      }],
      display: {
        opacity: 0,
        zIndex: -1
      },
      pc: true
    }
  },
  mounted() {
    const that = this
    if (document.body.clientWidth < 768 || document.body.clientHeight < 600) {
      that.pc = false
    }
    window.addEventListener('resize', function() {
      if (document.body.clientWidth < 768 || document.body.clientHeight < 600) {
        that.pc = false
      } else {
        that.pc = true
      }
    })
  },
  methods: {
    showBook() {
      this.display.opacity = 1
      this.display.zIndex = 1
    }
  }
}
</script>

<style scoped>
.book {
  position: absolute;
  height: 80vh;
  width: 60vh;
  left: 50%;
  top: 50%;
  transition: opacity .5s ease-in;
  transform: translateY(-50%);
}
.background {
  position: absolute;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
  background:linear-gradient(top, rgb(203, 235, 219) 0%, rgb(55, 148, 192) 120%);
}
.tip {
  height: 100%;
  width: 200%;
  transform: translateX(-50%);
}
</style>

