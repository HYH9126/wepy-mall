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
    在上述代码23行，setData会触发重新渲染，但并不会改变data.isHidden的值。
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

3——2018-06-01 问题:使用属性绑定操作符：时，wepy将：编译为v-bind:属性名.once，小程序不认识直接报错。
    原因分析：后来发现在页面中引入的自定义组件标签内使用：绑定属性，wepy就可以正确的编译并绑定属性，猜测原因是小程序原生组件不支持：操作符，并且wepy也没有修改原生组件让其支持，但wepy自定义组件就支持了：操作符。
    解决办法：原生组件不用：操作符，自定义组件用。

4——2018-06-04 问题：使用scroll-view组件的横向滚动功能scroll-x时，遇到整个页面也可以横向左右小幅度滑动的问题。
    原因分析：在尝试了阻止movetouch事件冒泡无果(一阻止就全部阻止，导致页面无法上下滑动)后猜测问题产生原因是因为scroll-view宽度超出750，导致在整个页面从最外层到最内层的结构都能捕获到movetouch事件的左右滑动，此情况应该与scroll-view组件无关，但凡有模块超750宽度应该都会产生此问题。
    解决办法：将scroll-view宽度定死为750rpx即可。

5——2018-06-04
