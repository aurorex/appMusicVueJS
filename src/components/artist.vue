<template lang="pug">
  li(class="artist")
    h2: a(:href="artist.url" target="_blanck") {{artist.name}}
    //- el ['#text'] es un atributo de tamaño del url del json ; los atributos se deben indicar de esa manera
    img(:src="artist.image[2]['#text']")
  
</template>

<script>
  export default {
    // nombre del tag:
    name: 'artist',
    // la propiedad es un array:
    props: ['artist']
    
  }
</script>

<style lang="stylus" scoped>
  li.artist
    display block
    margin 10px 0
  
</style>
