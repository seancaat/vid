<template>
  <div class="container">
    <h1>{{ data.name }}</h1>
    <main>
      <video ref="video" @timeupdate="currentTime_ = $event.target.currentTime" src="@/assets/videos/hillary.mp4" controls></video>
      <form>
        <label for="start">Start</label>
        <input type="text" id="start" name="start">

        <label for="end">End</label>
        <input type="text" id="end" name="end">

        <input type="submit" value="Focus timeframe" @click.prevent="trim">
      </form>
    </main>
    <section class="data">
      <h2>Metadata</h2>
      <DataViz :start="this.trimStart" :end="this.trimEnd" />
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
      trimStart: 0,
      trimEnd: 0,
    };
  },
  methods: {
    trim() {
      this.trimStart = document.getElementById("start").value;
      this.trimEnd = document.getElementById("end").value;
      console.log(this.trimStart);
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
  border: 1px solid red;
  max-width: 80%;
  box-sizing: border-box;
  padding: 1em;
  
  main {
    display: flex;
    video {
      max-width: 80%;
    }
    form {
      max-width: 20%;
      padding: 1em;

      input, label {
        display: block;
      }

      input {
        margin-bottom: 1em;
      }
    }
  }
}

</style>
