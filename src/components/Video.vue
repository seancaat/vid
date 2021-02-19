<template>
  <div class="container">
    <h1>{{ data.name }}</h1>
    <main>
      <video ref="video" @timeupdate="currentTime_ = $event.target.currentTime" src="@/assets/videos/hillary.mp4" controls></video>
      <!-- :max set to this.duration was getting a weird cannot set a read only issue -->
      <label for="start">Start</label>
      <input value="10" min="0" :max="476.821769" step="1" type="range" @change="updateStart">
      <label for="end">End</label>
      <input value="10" min="0" :max="476.821769" step="1" type="range" @change="updateEnd">
    </main>
    <section class="data">
      <h2>Metadata</h2>
      <DataViz :start="this.start" :end="this.end" />
    </section>
  </div>
</template>

<script>
import data from "@/data/sample.json"
import DataViz from "@/components/DataViz.vue"

export default {
  name: "Video",
  components: {
    DataViz
  },
  data() {
    return {
      data: data.metadata,
      start: 0,
      end: 476.821769,
      trimStart: 0,
      trimEnd: 0,
      duration: 0
    };
  },
  mounted () {
    document.querySelector("video").addEventListener('loadedmetadata', function(e) {
      console.log(e.target.duration);
    });

    this.$refs.video.addEventListener('timeupdate', (event) => {
      if(this.$refs.video.currentTime > this.end) {
        this.$refs.video.currentTime = this.start;
      }
    });
  },
  methods: {
    updateStart(e) {
    	this.start = e.target.value;
      this.$refs.video.currentTime = this.start;
      console.log(this.start)
    },
    
    updateEnd(e) {
    	this.end = e.target.value;
      console.log(this.end)
    },

    trim() {
      this.trimStart = document.getElementById("start").value;
      this.trimEnd = document.getElementById("end").value;
    },

    loop() {
      this.$refs.video
    }

  },
  computed: {
    	currentTime: {
        get: ({ currentTime_ }) => currentTime_,
        set(time) {
        	this.$refs.video.currentTime = time
        }
      }
    }
};
</script>

<style scoped lang="scss">

.container {
  margin: 0 auto;
  max-width: 80%;
  box-sizing: border-box;
  padding: 1em;
  
  main {
    // display: flex;
    video {
      max-width: 100%;
    }
    input[type=range] {
      display: block;
      width: 100%;
    }
    input {
      margin-top: 1em;
    }
  }
}

</style>
