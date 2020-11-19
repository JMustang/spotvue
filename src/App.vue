<template>
  <div id="app">
    <header>
      <h1>Spotvue</h1>
    </header>
    <main>
      <section class="Player">
        <div class="current__song">
        <h2 class="song-title"><h6>tocando</h6>{{ current.title }} - <span>{{ current.artist }}</span></h2>
        </div>
        <div class="contros">
        <button class="prev" @click="prev">Prev</button>
        <button class="play" v-if="!isPlaying"  @click="play">Play</button>
        <button class="pause" v-else  @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
        </div>
      </section>

      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-for="song in songs" 
        :key="song.src" 
        @click="play(song)" 
        :class="(song.src == current.src) 
        ? 'song playing' : 'song'">
           {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>



<script>
export default {
  name: 'App',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Alive',
          artist: 'Pearl Jam',
          src: require('./assets/Alive.mp3')
        },
        {
          title: 'Black',
          artist: 'Pearl Jam',
          src: require('./assets/Black.mp3')
        }
      ],
      Player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;

        this.Player.src = this.current.src;
      }

      this.Player.play();
      this.isPlaying = true;
    },
    pause () {
      this.Player.pause();
      this.isPlaying = false;
    },

    next () {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev () {
      this.index--;
      if (this.index < this.songs.length - 1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },


  created () {
    this.current = this.songs[this.index];
    this.Player.src = this.current.src;
  }
}
</script>



<style>
 * {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
 }
 body {
   font-family: sans-serif;
 }
 header {
   display: flex;
   font-family: 'Press Start 2P', cursive;
   justify-content: center;
   align-items: center;
   padding: 15px;
   background-color: #212121;
   color: #fff;
 }
 main {
   background-color: #bf3a30;
background-image: linear-gradient(315deg, #bf3a30 0%, #864ba2 74%);


   width: 100%;
   max-width: 768px;
   margin: 0 auto;
   padding: 25px;
 }
 h6 {
   color: #CC2E5D;
 }
 .current__song {
   border-radius: 25px;
   padding: 15px;
   background-color: #212121;
 }
 .song-title {
   color: #a201ff;
   font-size: 32px;
   font-weight: 700;
   text-transform: uppercase;
   text-align: center;
 }
 .song-title span {
   font-weight: 400;
   font-style: italic;
 }
 .contros {
   display: flex;
   justify-content: center;
   align-items: center;
   padding: 30px 15px;
 }
 button {
   appearance: none;
   background: none;
   border: none;
   outline: none;
   cursor: pointer;
 }
 button:hover {
   opacity: 0.8;
 }
 .play, .pause {
   font-size: 20px;
   font-weight: 700;
   padding: 15px 25px;
   margin: 0px 15px;
   border-radius: 8px;
   color: #fff;
   background-color: #CC2E5D;
 }
 .next, .prev {
   font-size: 16px;
   font-weight: 700;
   padding: 10px 20px;
   margin: 0px 15px;
   border-radius: 6px;
   color: #fff;
   background-color: #FF5858;
 }
 .playlist {
   padding: 0px 30px;
 }
 .playlist h3 {
   color: #212121;
   font-size: 28px;
   font-weight: 400;
   margin-bottom: 30px;
   text-align: center;
 }
 .playlist .song {
   display: block;
   width: 100%;
   padding: 15px;
   font-size: 20px;
   font-weight: 700;
   cursor: pointer;
 }
 .playlist .song:hover {
   color: #FF5858;
 }
 .playlist .song.playing {
   color: #fff;
   background-image: linear-gradient(to right, #cc2e5d,);
 }
</style>

