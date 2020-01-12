<template>
  <div class="Songs">
    <div class="column-row">
      <div class="column">   
        <img :src="this.songInfo.album.images[0].url" width="150" height="150">
          </div>
            <div class="column">
              <pre>
                  <a :href=this.songInfo.external_urls.spotify style="color: #8ebf42">{{this.songInfo.name}}</a>
                  by {{this.songInfo.artists[0].name}}
                  {{this.songInfo.album.name}}
              </pre>
          </div>
      </div>
  </div>
</template>


<script>
export default {
    name: "Song",
    props: {
        songInfo: null,
    },
};
</script>