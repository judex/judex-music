<template>
  <div id="app">
    <img src="/judex-music/dist/logo.png" width="30">
    <h1>{{ msg }}</h1>
    <select name="" v-model="selectedcountry">
      <option v-for="(country, index) in countries" :key="index" :value="country.value">
        {{ country.name }}
      </option>
    </select>
    <hr/>
    <Loader v-show="loading"></Loader>
    <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid"></artist>
  </div>
</template>

<script>
import Artist from './components/Artist'
import getArtists from './api'
import Loader from './components/Loader'
export default {
  name: 'app',
  data () {
    return {
      msg: 'Bienvenido a judexmusic',
      artists: [],
      countries: [
        { name: 'Perú', value: 'peru' },
        { name: 'China', value: 'china' },
        { name: 'España', value: 'spain' },
        { name: 'Bolivia', value: 'bolivia' },
      ],
      selectedcountry: 'peru',
      loading: false,
    }
  },
  components: {
    Artist, Loader
  },
  methods: {
    refresArtist(){
      const self = this
      this.loading = true
      this.artists =  []
      getArtists(this.selectedcountry)
        .then(function (artists){
          self.loading = false
          self.artists = artists
        })
    }
  },
  mounted() {
    this.refresArtist()
  },
  watch:{
    selectedcountry(){
      this.refresArtist()
    }
  }
}
</script>
<style lang="scss">
*{
  padding: 0;
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
select{
  width: 20%;
  padding: 10px 16px;
}
hr{
  margin-top: 20px;
  margin-bottom: 15px;
}
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
