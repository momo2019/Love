<template>
  <div class="wrap" :style="style" @click="handleTurn">
    <div v-if="isFirst" class="page" style="background: #eadedf;">
      <div class="fm" :style="{'backgroundImage': 'url(' + font.img + ')'}" />
      <div class="text-box">
        <div>{{ font.title }}</div>
      </div>
    </div>
    <div v-else class="page font">
      <div>
        <div class="litte-title">{{ font.title }}</div>
      </div>
      <div class="title">
        {{ font.title }}
      </div>
      <div class="content">
        <p v-for="(item, index) in contents" :key="index">{{ item }}</p>
      </div>
      <div class="image" :style="{'backgroundImage': 'url(' + font.img + ')'}">
      </div>
      <div class="index">{{ font.index }}</div>
    </div>
    <div class="page back" :style="{'backgroundImage': 'url(' + back.img + ')'}">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Page',
  props: {
    isFirst: {
      type: Boolean
    },
    index: {
      type: Number
    },
    sum: {
      type: Number
    },
    font: {
      type: Object
    },
    back: {
      type: Object
    }
  },
  data () {
    return {
      style: {
        transform: 'perspective(1000px) rotateY(0deg)',
        zIndex: 0
      },
      flag: true,
      contents: []
    }
  },
  created() {
    this.style.zIndex = this.sum - this.index
    this.handleContent()
  },
  methods: {
    handleTurn() {
      if (!this.flag){
        return false
      } 
      if (this.style.transform === 'perspective(1000px) rotateY(0deg)') {
        this.style.transform = 'perspective(1000px) rotateY(-180deg)'
        this.flag = false
        setTimeout(_ => {
          this.style.zIndex = this.index
        }, 1000)
        setTimeout(_ => {
          this.flag = true
        }, 3000)
      } else {
        this.style.transform = 'perspective(1000px) rotateY(0deg)'
        this.flag = false
        setTimeout(_ => {
          this.style.zIndex = this.sum  - this.index
        }, 800)
        setTimeout(_ => {
          this.flag = true
        }, 3000)
      }
    },
    handleContent() {
      const temp = this.font.content
      if (temp) {
        const data = temp.split('_')
        this.contents = data
      }
    }
  }
}
</script>

<style scoped>
.wrap {
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
  transition: transform 3s;
  transform-origin: left center;
  transform-style: preserve-3d;
  background-color: #fff;
  box-shadow: 0 3px 15px rgba(0, 0, 0, 0.2);
}
.page {
  position: absolute;
  height: 100%;
  width: 100%;
  backface-visibility: hidden;
  padding: 20px 40px;
  box-sizing: border-box;
  background: #fff;
}
.font {
  box-shadow: inset 30px 0 50px -30px rgba(0, 0, 0, 0.4);
}
.back {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  transform: rotateY(180deg) translateZ(1px);
  box-shadow: inset -30px 0 60px -30px rgba(0, 0, 0, 0.5);
}
.page .litte-title {
  height: 25px;
  width: 140px;
  margin: 10px 10px 0 auto;
  text-align: right;
  font-size: 12px;
}
.page .litte-title::after{
  content: '';
  display: block;
  height: 2px;
  width: 100%;
  background: linear-gradient(to left, #444 30%, #fff 90%);  
}
.page .title {
  height: 24px;
  width: 100%;
  margin: calc(30% - 65px) 0;
  text-align: left;
  font-size: 18px;
}
.page .content {
  height: 120px;
  width: 100%;
  padding-left: 20px;
  font-size: 12px;
  box-sizing: border-box;
}
.page .content > p {
  margin: 0;
}
.page .image {
  height: 30%;
  width: 100%;
  margin-top: 30px;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}
.page .index {
  width: 100%;
  margin-top: 10%;
  padding: 0 10px;
  text-align: right;
  font-size: 12px;
  box-sizing: border-box;
}
.page .fm {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 50%;
  background-size: cover;
  background-position-y: center;
}
.page .text-box {
  position: absolute;
  left: 0;
  top: 50%;
  width: 100%;
  height: 50%;
}
.page .text-box > div:nth-child(1) {
  margin-top: 40px;
  text-align: center;
  font-size: 30px;
  font-weight: 300;
}
</style>

