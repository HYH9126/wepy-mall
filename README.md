<<<<<<< .mine

1——2018-05-30 问题：<scroll-view>组件中的事件，scrolltoupper 、scrolltolower事件在wepy中不会触发。
    解决办法：原因不明，没查到此同样的问题，弃用<scroll-view>组件，改用<view>及onPageScroll事件。


2——2018-06-01 问题：
    export default class Index extends wepy.page {
        data = {
        isHidden: true,
        indicatorDots: true,
        indicatorActiveColor: '#fff',
        interval: 3000,
        duration: 1000,
        circular: true,
        adList: analogData.adData
        }

        onLoad() {
        console.log('onLoad')
        }
        onPageScroll(e) {
        if (e.scrollTop >= 325 && this.data.isHidden) {
            console.log('显示')
            this.setData({
            isHidden: false
            })
            console.log('===>hiddenFlag1:' + this.data.isHidden)
        }
        if (e.scrollTop < 325 && !this.data.isHidden) {
            console.log('隐藏')
            this.setData({
            isHidden: true
            })
            console.log('===>hiddenFlag2222:' + this.data.isHidden)
        }
        }
    }
    在上述代码中，setData会触发重新渲染，但并不会改变data.isHidden的值。
    解决办法：看官方文档后也无法实现，文档有问题。看官方demo后修改为入下代码解决。
    export default class Index extends wepy.page {
        data = {
        isHidden: true,
        indicatorDots: true,
        indicatorActiveColor: '#fff',
        interval: 3000,
        duration: 1000,
        circular: true,
        adList: analogData.adData
        }

        methods = {
        onPageScroll(e) {
            if (e.scrollTop >= 325 && this.isHidden) {
            console.log('显示')
            this.isHidden = false
            console.log('===>hiddenFlag1:' + this.isHidden)
            }
            if (e.scrollTop < 325 && !this.isHidden) {
            console.log('隐藏')
            this.isHidden = true
            console.log('===>hiddenFlag2222:' + this.isHidden)
            }
        }
        }

        onLoad() {
        console.log('onLoad')
        }
    }

3——2018-06-01 问题:
=======
# wepy-mall
学一下小程序，朋友推荐用wepy框架，顺带一起学了





































































>>>>>>> .theirs
