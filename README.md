基于贝塞尔曲线的手写签名，用于微信小程序
使用方法：

```
<canvas type="2d" disable-scroll="true" bindtouchstart="handleTouchStart" bindtouchmove="handleTouchMove" bindtouchend="handleTouchEnd" id="myCanvas"></canvas>

data: {
    signaturePad: new SignaturePad(),
},

handleTouchStart(event) {
    this.data.signaturePad._handleTouchStart(event)
},

handleTouchMove(event) {
    this.data.signaturePad._handleTouchMove(event)
},

handleTouchEnd(event) {
    this.data.signaturePad._handleTouchEnd(event)
},

onReady: function () {
    const query = wx.createSelectorQuery()
    query.select('#myCanvas')
        .fields({ node: true, size: true })
        .exec((res) => {
            const canvas = res[0].node
            const ctx = canvas.getContext('2d')
            const dpr = wx.getSystemInfoSync().pixelRatio
            canvas.width = res[0].width * dpr
            canvas.height = res[0].height * dpr
            ctx.scale(dpr, dpr)
            this.data.signaturePad._init(canvas)
        })
    // const signaturePad = new SignaturePad(context)
},
```
