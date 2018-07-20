<template>
  <div class="item-drag" :style="itemStyleObj" @mousedown="eleMove" @dblclick="dblclickHandle">
    <slot></slot>
  </div>
</template>
<style scoped>
  .item-drag:focus {
    outline: none;
  }
</style>
<script>
  export default {
    name: 'item-drag',
    data () {
      return {}
    },
    props: {
      width: {
        type: Number,
        default: 100
      },
      height: {
        type: Number,
        default: 100
      },
      border: {
        type: String,
        default: '1px solid black'
      }
    },
    mounted () {
      this.$nextTick(function () {
        let eles = document.querySelectorAll('.item-drag');
        [].forEach.call(eles, function (item, index) {
          item.style.left = `${this.width*index + 20}px`
        }.bind(this))
//        for (let key in eles) {
//          console.log(key)
//          eles[key].style && (eles[key].style.left = `${this.width}px`)
//        }
      })
    },
    methods: {
      dblclickHandle () {
        console.log('触发了双击事件')
      },
      eleMove (e) {
        // 获取父元素
        let parentEle = document.querySelector('.main-drag')
        // 获取所有的元素
        let eles = document.querySelectorAll('.item-drag')
        // 获取当前点击的元素
        let ele = e.target
        // 获取其他元素
      let otherEles = [].filter.call(eles, p => p != ele)
//      // 保存起始位置
      let startLeft = ele.offsetLeft
      let startTop = ele.offsetTop
//      // 获取鼠标在元素上点击的位置
      let mouseX = e.clientX - ele.offsetLeft
      let mouseY = e.clientY - ele.offsetTop
        // 注册鼠标抬起事件
        parentEle.onmouseup = function (e) {
          let left = e.clientX - mouseX
          let top = e.clientY - mouseY
          for (let key in otherEles) {
            let eleLeft = otherEles[key].offsetLeft
            let eleTop = otherEles[key].offsetTop
            let diffLeft = eleLeft > left ? eleLeft - left : left - eleLeft
            let diffTop = eleTop > top ? eleTop - top : top - eleTop
            if (diffLeft <= ele.offsetWidth && diffTop <= ele.offsetHeight) {
              parentEle.onmousemove = null
              parentEle.onmousemove = null
              ele.style.transition = 'all 1s'
              ele.style.position = 'absolute'
              ele.style.left = `${eleLeft}px`
              ele.style.top = `${eleTop}px`
              otherEles[key].style.transition = 'all 1s'
              otherEles[key].style.left = `${startLeft}px`
              otherEles[key].style.top = `${startTop}px`
              return false
            }
          }
          parentEle.onmousemove = null
          parentEle.onmousemove = null
        }
//      // 注册鼠标移动事件
      parentEle.onmousemove = function (e) {
        let left = e.clientX - mouseX
        let top = e.clientY - mouseY
        ele.style.transition = ''
        ele.style.position = 'absolute'
        ele.style.left = `${left}px`
        ele.style.top = `${top}px`
      }
      }
    },
    computed: {
      itemStyleObj () {
        return {
          width: `${this.width}px`,
          height: `${this.height}px`,
          border: this.border,
          position: 'absolute'
        }
      }
    }
  }
</script>
