<template>
    <div class="main-artist">
      <a :href="artist.url" target="_blank">
        <img :src="artist.image[2]['#text']" alt="">
        <h5>{{ artist.name }}</h5>
      </a>
    </div>
</template>

<script>
  export default {
    name: 'artist',
    props: [ 'artist' ]
  }
</script>

<style lang="scss" scoped>
.main-artist{
  display: inline-block;
  margin-bottom: 30px;
  ul, li{
    list-style: none;
    padding: 0;
    margin: 0;
  }
  li{
    float: left;
  }
  a{
    padding: 5px;
    border: 2px solid #ccc;
    background: #f4f4f4;
    display: inline-block;
    margin-left: 15px;
    margin-right: 15px;
    transition: .3s all;
    filter: grayscale(100%);
    &:hover{
      filter: grayscale(0%);
      border-color:#42b9a0;
    }
  }
}
</style>

