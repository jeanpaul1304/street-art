<template>
  <v-container grid-list-md text-xs-center>
    <v-slide-y-transition mode="out-in">
      <v-layout row wrap>
        <v-flex xs8>
          <gmap-map
            :center="center"
            :zoom="11"
            style="width: 500px; height: 300px"
          >
            <gmap-marker
              :key="index"
              v-for="(m, index) in markers"
              :position="m.position"
              :clickable="true"
              @click="showInfo(index)"
            ></gmap-marker>
          </gmap-map>
        </v-flex>

        <v-flex xs4>
          <h2>{{currentInfo.title}}</h2>
          <p>{{currentInfo.desc}}</p>
          {{currentInfo}}
        </v-flex>
        <br>
      </v-layout>
    </v-slide-y-transition>
  </v-container>
</template>

<script>
  import Vue from 'vue'
  import * as VueGoogleMaps from 'vue2-google-maps'
  import {pins} from '../assets/model/pin'
  Vue.use(VueGoogleMaps, {
    load: {
      key: 'AIzaSyDzY0Z7aSitGJI4svmlaKcTX49mVoVfY0Y',
      libraries: 'places', // This is required if you use the Autocomplete plugin
      // OR: libraries: 'places,drawing'
      // OR: libraries: 'places,drawing,visualization'
      // (as you require)
    }
  })
  let vm
  export default {
    mounted() {
      vm = this
    },
    data () {
      return {
        pin: pins,
        center: {lat: -12.0509118, lng: -77.0698077},
        markers: pins,
        currentInfo: ''
      }
    },
    methods: {
      showInfo(index) {
        vm.center= vm.markers[index].position
        vm.currentInfo = vm.markers[index].data
      }
    }
  }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>


<!--<v-card>-->
  <!--<v-card-media src="/static/news/ppk.jpg" height="200px">-->
  <!--</v-card-media>-->
  <!--<v-card-title primary-title>-->
    <!--<div>-->
      <!--<h3 class="headline mb-0">Chofer de PPK recibe 700,000 USD</h3>-->
      <!--<div>Se encontró que PPK habría deribado a su chofer montos que ascienden a 700,000 dolares...</div>-->
    <!--</div>-->
  <!--</v-card-title>-->
  <!--<v-card-actions align-content-end>-->
    <!--<v-btn flat color="orange">Compartir</v-btn>-->
    <!--<v-btn flat color="orange">Ver registro</v-btn>-->
  <!--</v-card-actions>-->
<!--</v-card>-->
<!--<br>-->
<!--<v-card>-->
  <!--<v-card-media src="/static/news/puente.jpg" height="200px">-->
  <!--</v-card-media>-->
  <!--<v-card-title primary-title>-->
    <!--<div>-->
      <!--<h3 class="headline mb-0">Indicios de corrupción en Puente Bella Unión</h3>-->
      <!--<div>Se encontró que PPK habría deribado a su chofer montos que ascienden a 700,000 dolares...</div>-->
    <!--</div>-->
  <!--</v-card-title>-->
  <!--<v-card-actions align-content-end>-->
    <!--<v-btn flat color="orange">Compartir</v-btn>-->
    <!--<v-btn flat color="orange">Ver registro</v-btn>-->
  <!--</v-card-actions>-->
<!--</v-card>-->
