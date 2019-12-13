<template>
  <div>
    <div>
      <div>
        <span>这里输入ezopen地址： </span>
        <input type="text" class="input" v-model="ezopenUrl">
      </div>
      <div>
        <span>这里输入accessToken： </span>
        <input type="text" class="input"  v-model="token">
      </div>
    </div>

    <div class="btn-container">
      <button @click="onInit" id="init">初始化播放</button>
      <button @click="onStop" id="stop">结束</button>
      <button id="getOSDTime">获取OSD时间</button>
      <button id="openSound">打开声音（默认已经开启）</button>
      <button id="closeSound">关闭声音</button>
      <button id="capturePicture">视频截图</button>
      <button id="startSave">开始录像</button>
      <button id="stopSave">停止录像</button>
      <span>
        录制功能不支持加密视频，且录制的文件需要
        <a href="https://service.ys7.com/downloadInfoSite/admin" target="_blank">下载海康播放器播放</a>
      </span>
    </div>
    <div id="playWind" style="width: 600px; height: 400px;"></div>
  </div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
      decoder: null,
      ezopenUrl: '',
      token: '',
    };
  },
  watch: {},
  computed: {},
  methods: {
    onInit(e){
      console.log('onInit', e)            
      function handleError(e){
        console.log('handleError',e)
      }
      function handleSuccess(){
        console.log('handleSuccess')
      }
      this.decoder = new EZUIKit.EZUIPlayer({
        id: 'playWind',
        autoplay: true,
        url: this.ezopenUrl,
        accessToken: this.token,
        decoderPath: '/static/ezui',
        width: 600,
        height: 400,
        handleError: handleError,
        handleSuccess: handleSuccess,
      });
    },
    onStop(e){
      console.log('onStop', e)
      this.decoder.stop();
    }
  },
  created() {},
  mounted() {}
};
</script>
<style scoped>
#playWind{
  align-content: center;
  margin: 10px auto;
}
.input{
  width: 500px;
  margin-bottom: 15px;
}
</style>