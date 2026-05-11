<template>
  <div class="player-wrapper">
    <video ref="videoPlayer" class="video-js vjs-default-skin" controls></video>
  </div>
</template>

<script>
import videojs from 'video.js'
import 'video.js/dist/video-js.css'
// Note: video.js v7+ includes http-streaming by default,
// but keeping the import is fine for older setups.
import '@videojs/http-streaming'

export default {
  name: 'MpdPlayer',
  data() {
    return {
      player: null,
    }
  },
  methods: {
    getStream() {
      this.player = videojs(this.$refs.videoPlayer, {
        autoplay: false,
        fluid: true,
        sources: [
          {
            src: 'http://136.239.173.2:6610/001/2/ch00000090990000001087/manifest.mpd?AuthInfo=v87HD9rEhwHiAdYyrP20Tg5pgSMSITY%2FHYvvCWJRp%2BqHRrK8UUahwItHhKpXgPXKytokK1MIobcue1ImXa0ZEA%3D%3D&version=v1.0&BreakPoint=0&virtualDomain=001.live_hls.zte.com&programid=ch00000000000000001176&contentid=ch00000000000000001176&videoid=ch00000090990000001087&recommendtype=0&userid=1287297673984&boid=001&stbid=02%3A00%3A00%3A00%3A00%3A00&terminalflag=1&profilecode=&usersessionid=U4DB4Z0H2EXXXX&NeedJITP=1&JITPMediaType=DASH&JITPDRMType=NO',
          },
        ],
      })
    },
  },
  mounted() {
    this.getStream()
  },
  beforeUnmount() {
    if (this.player) {
      this.player.dispose()
    }
  },
}
</script>

<style scoped>
.player-wrapper {
  width: 100%;
  max-width: 900px;
}
</style>
