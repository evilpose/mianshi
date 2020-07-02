<template>
  <div id="app">
    <header v-if="screen === 1">
      <nav>
        <div class="left"></div>
        <div class="main">
          <span>HOME</span>
          <span>NEWS</span>
          <span>WEAPONS</span>
          <span>MAP</span>
          <span class="activeSpan">CHARACTERS</span>
          <span>WALLPAPER</span>
        </div>
        <div class="right"></div>
      </nav>
      <img class="title" src="@/assets/logo.png" alt="">
    </header>
    <article v-if="screen === 1">
      <div class="CHARACTER">
        <div class="hexagon">
          <span>CHARACTERS</span>
        </div>
      </div>
      <div class="articleMain">
        <!-- 这儿应该使用 v-for 渲染 -->
        <img src="@/assets/1.jpg">
        <img src="@/assets/2.jpg">
        <img src="@/assets/3.jpg">
        <img src="@/assets/4.jpg">
        <img src="@/assets/4.jpg">
        <div>
          <img src="@/assets/1.jpg">
          <img src="@/assets/2.jpg">
          <img src="@/assets/3.jpg">
          <img src="@/assets/4.jpg">
        </div>
      </div>
    </article>
    <div class="Mask" v-if="screen === 0">
      <img src="@/assets/scape.png">
      <p>请使用横屏访问</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      screen: 0,
      // 使用main和children分批次渲染
      dataList: {
        main: [
          'xxxx', 'xxx', 'xxx', 'xxx', 'xxx'
        ],
        children: [
          'xxxx', 'xxx', 'xxx', 'xxx'
        ]
      }
    }
  },
  created () {
    // 使用原生的请求去获取数据
    const url = 'http://rap2.taobao.org:38080/app/mock/259764/get/dataList'
    const xhr = new XMLHttpRequest()
    xhr.open('GET', url)
    xhr.send()
    xhr.onload = function () {
      if (this.status === 200) {
        console.log('下面就是拿到了数据')
        console.log(this.response)
        // 拿到了数据再交给上面去渲染
      } else if (this.status === 404) {
        console.log('错误')
      } else {
        console.log('加载失败')
      }
    }
  },
  beforeMount () {
    window.addEventListener('orientationchange', () => {
      if (window.orientation === 0) {
        // 竖屏
        this.screen = 0
      }
      if (window.orientation === 90) {
        // 横屏
        this.screen = 1
      }
    }, false)
  }
}
</script>

<style lang="scss">
  @import './App.scss'
</style>
