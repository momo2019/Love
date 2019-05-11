<template>
  <div style="width: 100%; height: 100%; font-size: 0px;">
    <div class="tip-box left">
      <div class="tip-content tip1"></div>
    </div>
    <div class="tip-box right">
      <div class="tip-content tip2"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tip'
}
</script>

<style scoped>
.tip-box {
  position: relative;
  display: inline-block;
  height: 100%;
  width: 50%;
  padding: 40px 30px;
  font-size: 20px;
  box-sizing: border-box;
}
.tip-content {
  position: absolute;
  height: 200px;
  width: 100%;
  left: 50%;
  top: 50%;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  transform: translateX(-50%) translateY(-50%);
}
.tip1 {
  background-image: url('../image/fanye.png')
}
.tip2 {
  background-image: url('../image/npy.png')
}
</style>
