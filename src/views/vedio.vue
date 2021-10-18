<!--
 * @Autor: 卢建
 * @LastEditors: 卢建
 * @Description: 视频
 * @Date: 2021-09-07 15:52:01
 * @LastEditTime: 2021-09-17 17:06:54
-->
<template>
  <div>
    <div id="dplayer" ref="player"></div>
  </div>
</template>

<script>
import Hls from "hls.js";
import Dplayer from "dplayer";

export default {
  name: "dplayer",
  data() {
    return {
      dp: null,
      video: {
        img: require("../assets/404.jpg"),
        video: "http://192.168.3.173:8080/hls/test.m3u8",
      },
    };
  },
  methods: {
    loadVideo(videoInfo) {
      this.dp = new Dplayer({
        element: this.$refs.player,
        video: {
          pic: videoInfo.img, // 封面
          url: videoInfo.video,
          type: "customHls",
          customType: {
            customHls: function (video, player) {
              const hls = new Hls();
              hls.loadSource(video.src);
              hls.attachMedia(video);
            },
          },
        },
        autoplay: true,
      });
    },
  },
  mounted() {
    this.loadVideo(this.video);
  },
};
</script>
<style scoped>
#dplayer {
  width: 500px;
  height: 300px;
}
</style>