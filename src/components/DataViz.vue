<template>
    <figure>
      <figcaption>Current time: {{ }}.Metadata at time {{ start }} to {{ end }}</figcaption>
      <!-- segment based on video length? -->
      <svg version="1.1" 
      xmlns="http://www.w3.org/2000/svg" 
      xmlns:xlink="http://www.w3.org/1999/xlink" 
      class="chart" 
      aria-labelledby="title" 
      >

       <!--3 consider slider interface (double) -->
       <!--2 how many ocurrences / averages within time frame -->

      <!-- width = normalized difference between .start and .end -->
        <title id="title">Metadata </title>
        <g v-for="(item, index) in json.named_entities" v-bind:key="index" class="bar" >
          <rect @click="showMetadata(index)" :width="item.end - item.start" :height="20" :x="item.start * 2" :fill="colors1[Math.floor(Math.random() * colors1.length)]"></rect>
        </g>
        <!-- <g v-for="(item, index) in json.recognized_people" v-bind:key="item + index" class="bar" >
          <rect @click="showMetadata(index)" :width="item.end - item.start" :height="20" :x="item.start * 2" :y="20" :fill="colors2[Math.floor(Math.random() * colors2.length)]"></rect>
        </g> -->
      </svg>
      <p ref="metadataDisplay"></p>
    </figure>
</template>

<script>
import sample from "@/data/sample.json"

// const width = document.querySelector("svg").offsetWidth;

const Colors1 = [
'#F44336',
// '#FFEBEE',
// '#FFCDD2',
// '#EF9A9A',
// '#E57373',
// '#EF5350',
// '#F44336',
// '#E53935',
// '#D32F2F',
// '#C62828',
// '#B71C1C',
// '#FF8A80',
// '#FF5252',
// '#FF1744',
// '#D50000',
// '#E91E63',
// '#FCE4EC',
// '#F8BBD0',
// '#F48FB1',
// '#F06292',
// '#EC407A',
// '#E91E63',
// '#D81B60',
// '#C2185B',
// '#AD1457',
// '#880E4F',
// '#FF80AB',
// '#FF4081',
// '#F50057',
// '#C51162',
// '#9C27B0',
// '#F3E5F5',
// '#E1BEE7',
// '#CE93D8',
// '#BA68C8',
// '#AB47BC',
// '#9C27B0',
// '#8E24AA',
// '#7B1FA2',
// '#6A1B9A',
// '#4A148C',
// '#EA80FC',
// '#E040FB',
// '#D500F9',
// '#AA00FF',
// '#673AB7',
// '#EDE7F6',
// '#D1C4E9',
// '#B39DDB',
// '#9575CD',
// '#7E57C2',
// '#673AB7',
// '#5E35B1',
// '#512DA8',
// '#4527A0',
// '#311B92',
// '#B388FF',
// '#7C4DFF',
// '#651FFF',
// '#6200EA',
// '#3F51B5',
// '#E8EAF6',
// '#C5CAE9',
// '#9FA8DA',
// '#7986CB',
// '#5C6BC0',
// '#3F51B5',
// '#3949AB',
// '#303F9F',
// '#283593'
]

const Colors2 = [
   '#FFAB91',
  // '#FF8A65',
  // '#FF7043',
  // '#FF5722',
  // '#F4511E',
  // '#E64A19',
  // '#D84315',
  // '#BF360C',
  // '#FF9E80',
  // '#FF6E40',
  // '#FF3D00',
  // '#DD2C00',
  // '#795548',
  // '#EFEBE9',
  // '#D7CCC8',
  // '#BCAAA4',
  // '#A1887F',
  // '#8D6E63',
  // '#795548',
  // '#6D4C41',
  // '#5D4037',
  // '#4E342E',
  // '#3E2723',
  // '#9E9E9E',
  // '#FAFAFA',
  // '#F5F5F5',
  // '#EEEEEE',
  // '#E0E0E0',
  // '#BDBDBD',
  // '#9E9E9E',
  // '#757575',
  // '#616161',
  // '#424242',
  // '#212121',
  // '#607D8B',
  // '#ECEFF1',
  // '#CFD8DC',
  // '#B0BEC5',
  // '#90A4AE',
  // '#78909C',
  // '#607D8B',
  // '#546E7A',
  // '#455A64',
  // '#37474F',
  // '#263238'
]

export default {
  name: "DataViz",
  components: {
  },
  data() {
    return {
      json: sample.metadata,
      colors1: Colors1,
      colors2: Colors2
    };
  },
  props: ['start', 'end', 'currentTime'],
  methods: {
    normalizedDifference(start, end) {

    },
    map(a,b,c,d) {

    },
    showMetadata(index) {
      this.$refs.metadataDisplay.innerHTML = JSON.stringify(this.json.named_entities[index], null, 2);
    }
  }
};
</script>

<style scoped lang="scss">
figure {
  display: block;
  width: 100%;
  border: 1px solid black;
  margin: 0;

  figcaption {
    display: block;
    max-width: 100%;
  }

  p {
    max-width: 50%;
  }
}
svg {
  width: 100%;
  rect {
    stroke: white;

    &:hover {
      cursor: pointer;
      stroke: black;
      filter: saturate(200%);
    }
  }
}


</style>
