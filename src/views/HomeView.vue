<template>
  <div class="container">
    <div class="player_con">
      <div class="player_wrapper">
        <div ref="player_container"></div>
      </div>
    </div>
    <div class="channel_lists">
      <ul>
        <li v-for="(channel, index) in channels" :key="index">
          <button @click="getStream(channel.channelLink)">{{ channel.channelName }}</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import videojs from 'video.js'
import 'video.js/dist/video-js.css'
import '@videojs/http-streaming'
import channelLists from '../assets/js/channels.json'

export default {
  data() {
    return {
      defaultChannel: 'http://136.239.173.2:6610/001/2/ch00000090990000001087/manifest.mpd?AuthInfo=v87HD9rEhwHiAdYyrP20Tg5pgSMSITY%2FHYvvCWJRp%2BqHRrK8UUahwItHhKpXgPXKytokK1MIobcue1ImXa0ZEA%3D%3D&version=v1.0&BreakPoint=0&virtualDomain=001.live_hls.zte.com&programid=ch00000000000000001176&contentid=ch00000000000000001176&videoid=ch00000090990000001087&recommendtype=0&userid=1287297673984&boid=001&stbid=02%3A00%3A00%3A00%3A00%3A00&terminalflag=1&profilecode=&usersessionid=U4DB4Z0H2EXXXX&NeedJITP=1&JITPMediaType=DASH&JITPDRMType=NO',
      player: null,
      channels: channelLists,
    }
  },
  methods: {
    getStream(channelLink) {
      if (this.player) {
        this.player.dispose()
        this.player = null
      }

      const videoEl = document.createElement('video')
      videoEl.className = 'video-js vjs-default-skin'
      this.$refs.player_container.appendChild(videoEl)

      this.player = videojs(videoEl, {
        autoplay: true,
        fluid: true,
        sources: [{ src: channelLink}],
      })
    },
  }
}
</script>

<style scoped>
.container { display: flex; }
.player_wrapper { width: 100%; max-width: 900px; }
.player_con { width: 100%; max-width: 800px; }
</style>