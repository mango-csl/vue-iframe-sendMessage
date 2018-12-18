<template>
  <div class="act-form">
    <iframe :src="src"
      ref="iframe"></iframe>
    <!--<iframe src="../static/test.html" ref="iframe"></iframe>-->
    <div @click="sendMessage">向iframe发送信息</div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      src: '../static/test.html',
      iframeWin: {}
    }
  },
  methods: {
    sendMessage() {
      // 外部vue向iframe内部传数据
      this.iframeWin.postMessage({
        cmd: 'getFormJson',
        params: {}
      }, '*')
    },
    handleMessage(event) {
      // 根据上面制定的结构来解析iframe内部发回来的数据
      const data = event.data
      console.log('外部接受Iframe mes', data);
      switch (data.cmd) {
        case 'returnFormJson':
          // 业务逻辑
          break
        case 'returnHeight':
          // 业务逻辑
          break
      }
    }
  },
  mounted() {
    // 在外部vue的window上添加postMessage的监听，并且绑定处理函数handleMessage
    window.addEventListener('message', this.handleMessage)
    this.iframeWin = this.$refs.iframe.contentWindow
  }
}
</script>
