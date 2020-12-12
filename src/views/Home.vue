<template>
  <div class="container">
    
    <div class="center">
      <div class="icon">🚀</div>
      <div>{{box.text}}</div>
    </div>

    <p>Lorem ipsum dolor sit amet</p>

    <button @click.prevent="startRecording">Record</button>
    
    <div style="display: flex; flex-direction: row; height: 256px;">
      <div style="padding: 5px;">
        <video v-show="canRecord" autoplay="true" controls="true" />
      </div>

      <div style="padding: 5px;">
        <pre id="log"></pre>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'Home',
  computed: {
    canRecord() {
      return Object.keys(this.video || {}).length
    }
  },
  data: () => ({
    video: null,
    log: "",
    started: false,
    box: {
      text: 'Record your screen and share it with someone else, you can do realtime sharing with someone and you will be the one in control of what part of your screen you\'d want to be shared/recorded! When you\'re done you could alslo download the recording for even more use cases.'
    }
  }),

  mounted() {
    this.video = document.querySelector('video')
    this.log = document.querySelector('pre#log')
  },

  methods: {

    dumpOptionsInfo() {
      if (!this.video) {
        return
      }

      const videoTrack = this.video.srcObject.getVideoTracks()[0]
      
      if (videoTrack) {
        this.log.innerHTML += JSON.stringify(videoTrack.getSettings(), null, 2)
        this.log.innerHTML += JSON.stringify(videoTrack.getConstraints(), null, 2)


      }
      // console.info("Track settings:")
      // console.info(JSON.stringify(videoTrack.getSettings(), null, 2))
      // console.info("Track constraints:")
      // console.info(JSON.stringify(videoTrack.getConstraints(), null, 2))
    },

    async startRecording() {
        if (!this.canRecord) {
          return false
        }

       if (!('mediaDevices' in navigator)) {
        console.error('No mediaDevices!')
       }

        var displayMediaOptions = {
          video: {
            cursor: "always"
          },
          audio: false
        }


         this.video.srcObject = await navigator
           .mediaDevices
           .getDisplayMedia(displayMediaOptions)
           .then((ev) => {
             console.log({ ev })
             return ev
           })
          this.dumpOptionsInfo()


    }

  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  background: #ccc;
}

/* Track */
::-webkit-scrollbar-track {
  background: #f1f1f1;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #888;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #555;
}

pre#log {
  width: 50%px;
  height: 180px;
  flex: 1;
  align-items: stretch;
  margin: 0;
  padding: 0;
  background: #f1f1f1;
  border: 1px solid #ccc;
  overflow-y: scroll;
}

nav {
  width: 100%;
  height: 20px;
  background: rgba(0, 0, 0, 0.7);
  padding: 10px;
  color: whitesmoke;
  font-weight: bold;
  font-size: 1em;
}

video {
  width: 100%;
  height: 180px;
  border: 1px solid #000;
}

#app {
  background: white;
  border-bottom: 3px solid #888;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
  padding: 0 0 10px;
}

.center {
  display: flex;
  padding: 15px;
  text-align: left;
  border-left: 10px solid #4caf50;
  background: #000000ab;
  color: #f5f5f5;
  box-shadow: 0 3px 3px rgba(0,0,0,0.4);
  font-weight: bold;
  font-size: 1.1em;
}

.center .icon {
  font-size: 62px;
  margin-right: 15px;
}

.container {
  margin: 10px;
}
</style>
