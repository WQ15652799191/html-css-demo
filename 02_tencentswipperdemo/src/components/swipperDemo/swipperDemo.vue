<template>
  <div class="main">
    <div
    class="container"
    :style="'background-color:' + active_color + ';'"
  >
    <div
      class="banner"
      :style="'background-image:url('+active_image+');'"
    >
    </div>
    <div class="title-box">
      <div
      :class="['title', index == active_index ? 'active' : '']"
      :key="item.title"
      v-for="(item, index) in list"
      @mouseover="changeBanner(index)"
    >
      {{ item.title }}
      <span>{{ item.sub_title }}</span>
    </div>
    </div>
  </div>
  </div>
</template>
<script>
import one from '../../assets/1.jpg'
import two from '../../assets/2.jpg'
import three from '../../assets/3.jpg'
import four from '../../assets/4.jpg'
import five from '../../assets/5.jpg'
import six from '../../assets/6.jpg'
import seven from '../../assets/7.jpg'
import eight from '../../assets/8.jpg'
import nine from '../../assets/9.jpg'

export default {
  data () {
    return {
      list: [
        {
          title: '正在直播NBA',
          sub_title: '快船vs森林狼',
          image: one,
          bg_color: '#53839a'
        },
        {
          title: '特战荣耀·热播',
          sub_title: '杨洋展特种军魂',
          image: two,
          bg_color: '#bbbbaf'
        },
        {
          title: '王牌对王牌7',
          sub_title: '沈腾贾玲cos喜羊羊',
          image: three,
          bg_color: '#120f16'
        },
        {
          title: '军火大劫案',
          sub_title: '国版“史密斯夫妇”燃炸',
          image: four,
          bg_color: '#600004'
        },
        {
          title: '毛雪汪',
          sub_title: '李雪琴花式夸毛不易新歌',
          image: five,
          bg_color: '#eeec88'
        },
        {
          title: '狙击手的战争',
          sub_title: '乌克兰战争狙击手传奇',
          image: six,
          bg_color: '#89a1a3'
        },
        {
          title: '致命谋杀',
          sub_title: '揭秘连环杀手作案动机',
          image: seven,
          bg_color: '#1d221c'
        },
        {
          title: '现在就告白',
          sub_title: '健身教练告白女客户',
          image: eight,
          bg_color: '#bd60d5'
        },
        {
          title: '【海量福利】',
          sub_title: '诺亚之心上线领豪礼',
          image: nine,
          bg_color: '#0d283d'
        }
      ],
      active_index: 0,
      active_image: one,
      active_color: '#53839a',
      size: 9,
      timer: null
    }
  },
  methods: {
    startAutoplay () {
      const _this = this
      this.timer = setInterval(() => {
        _this.active_index++
        if (_this.active_index > _this.size - 1) {
          _this.active_index = 0
        }
        _this.changeBanner(_this.active_index)
      }, 2000)
    },
    stopAutoplay () {
      if (this.timer) {
        clearInterval(this.timer)
      }
    },
    changeBanner (index) {
      this.stopAutoplay()
      this.active_index = index
      this.active_image = this.list[index].image
      this.active_color = this.list[index].bg_color
      this.startAutoplay()
    }
  },
  mounted () {
    this.startAutoplay()
  }
}
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    /* 设置的边框和内边距的值时包含在总宽高内的 */
    box-sizing: border-box;
}
.main{
    /* 100%窗口高度 */
    height: 100vh;
    /* 弹性布局 居中显示 */
    display: flex;
    justify-content: center;
    align-items: center;
}
.container{
    /* 100%窗口宽度 */
    width: 100vw;
    /* 相对定位 */
    position: relative;
    /* 弹性布局 垂直排列 水平居中 */
    display: flex;
    flex-direction: column;
    align-items: center;
}
.banner{
    /* 90%窗口宽度 */
    width: 90vw;
    max-width: 1680px;
    height: 432px;
    background-size: cover;
    background-position: center;
}
.title-box{
    width: 348px;
    height: 432px;
    background-color: rgba(0,0,0,0.45);
    /* 绝对定位 右侧 */
    position: absolute;
    top: 0;
    right: 0;
    color: #fff;
    padding-top: 20px;
    /* 背景模糊 */
    backdrop-filter: blur(3px);
}
.title{
    height: 43px;
    line-height: 43px;
    text-indent: 40px;
    font-size: 15px;
    cursor: pointer;
    /* 文本不换行 */
    white-space: nowrap;
    /* 溢出隐藏 */
    overflow: hidden;
    /* 字体大小改变时的过渡 */
    transition: font-size 0.2s;
}
.title span{
    font-size: 13px;
    /* 副标题默认隐藏 */
    opacity: 0;
}
/* 当前项样式 */
.title.active{
    color: #ff5c38;
    font-size: 22px;
    font-weight: bold;
}
.title.active span{
    opacity: 1;
}
</style>
