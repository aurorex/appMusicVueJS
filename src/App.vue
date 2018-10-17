<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 {{ msg }}
    //- indicador de progreso:
    spinner(v-show="loading")
    //- cambiar segun lo que la gente escucha en cada pais
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value" ) {{country.name}}
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
      //- li( v-for="artist in artists") {{artist.name}} 
   
</template>

<script>
  import Artist from './components/artist.vue'
  import Spinner from './components/spinner.vue'

  import getArtists from './api'

  export default {
    name: 'app',
    data () {
      return {
        msg: 'Music App Vue',
        artists:[],
        countries:[
          {
            name:'Argentina', 
            value:'argentina'
          },
          {
            name:'Colombia', 
            value:'colombia'
          },
          {
            name:'Peru', 
            value:'peru'
          }

        ],
        selectedCountry:'argentina',
        loading: true
      }
    },
    components: {
      // con ecmascript 6
      Artist,
      Spinner
      // con ecmascript 5 
      // Artist: Artist
    },
    methods: {
      refreshArtists() {
        // en este caso this hace referencia al objeto window convenientemente
        // self hace referencia al componente!
        const self = this;
        this.loading = true
        getArtists(this.selectedCountry)
          .then(function(artists){
            self.loading = false
            self.artists = artists
          });
        
      }
    },
    mounted: function(){
      this.refreshArtists() 
    },
    // mounted(){
    //   this.refreshArtists()
      
    // },
    // objeto que  observa cuando hay un cambio para recien ejecutar la funcion
    watch: {
      selectedCountry: function() {
        this.refreshArtists()

      }
    }
  }
</script>

<style lang="stylus">
  #app
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    margin-top 60px

  h1, h2
    font-weight normal

  ul
    list-style-type none
    padding 0

  li
    display inline-block
    margin 0 10px

  a
    color #42b983
</style>
