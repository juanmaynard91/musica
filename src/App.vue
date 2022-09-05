<template>
  <header>
    <h1>MI MUSICA</h1>
  </header>

  <main>
    <section>
      <h2 style="text-transform: uppercase">{{ current.title }}</h2>
    </section>

    <div class="controles">
      <button class="prev bi bi-caret-left-fill" aria-label="prev" @click="prev"></button>
      <button class="play bi bi-play-fill" aria-label="play" v-if="!isPlaying" @click="play"></button>
      <button class="pause bi bi-pause-fill" aria-label="pause" v-else @click="pause"></button>
      <button class="next bi bi-caret-right-fill" aria-label="next" @click="next"></button>
    </div>

    <section class="playlist">
      <h2 style="text-decoration: underline">LISTA DE REPRODUCCION</h2>
      <button v-for="song in songs" :key="song.src" @click="play(song)"
        :class="song.src == current.src ? 'song playing' : 'song'">
        {{ song.title }}
      </button>
    </section>
  </main>

  <Footer />
</template>

<script>
import Footer from "@/components/Footer";
export default {
  name: "app",
  components: { Footer },

  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      player: new Audio(),
      songs: [
        {
          title: "Ace Aura Millennial Trash Self Sabotage",
          src: require("./assets/Ace Aura Millennial Trash Self Sabotage.mp3"),
        },
        {
          title: "Chime Ace Aura Interdimensional",
          src: require("./assets/Chime Ace Aura Interdimensional.mp3"),
        },
        {
          title: "Chime Bloom",
          src: require("./assets/Chime Bloom.mp3"),
        },
        {
          title: "Chime Pixel Perfect",
          src: require("./assets/Chime Pixel Perfect.mp3"),
        },
        {
          title: "Chime x Desembra x Tiigers Clockwor",
          src: require("./assets/Chime x Desembra x Tiigers Clockwor.mp3"),
        },
        {
          title: "Pixel Terror, Chime Teminite Sleepless",
          src: require("./assets/Pixel Terror, Chime Teminite Sleepless.mp3"),
        },
        {
          title: "Trivecta Wasteland",
          src: require("./assets/Trivecta Wasteland.mp3"),
        },
      ]
    };
  },

  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        // TYPEOF PARA SABER EL TIPO DE DATO
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current); //llamo al metodo play
    },

    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current); //llamo al metodo play
    },
  },

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play(); //CON ESTO REPRODUZCO LA MUSICA CADA VEZ QUE CARGO LA PAGINA
  },
};
</script>

<style>
:root {
  --color-letra: white;
  --color-fondo: black;
}
html,
body {
  background-size: 200% 200%;
  background-image: linear-gradient(
    to bottom right,
    #4affde 0%,
    #5b9dff 40%,
    #d06bff 60%,
    #ff34d2 100%
  );
  width: 100%;
  height: 100vh;
  text-align: center;
  font-family: "Oswald", sans-serif;
  animation: moving 5s linear infinite alternate;
}
@keyframes moving {
  from {
    background-position: 0, 0;
  }
  to {
    background-position: 100% 100%;
  }
}
h1,
h2 {
  color: var(--color-letra);
}
header {
  background: black;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 0.5rem;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.controles {
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
.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0 15px;
  border-radius: 8px;
  color: var(--color-letra);
  background: var(--color-fondo);
}
button:hover {
  opacity: 0.8;
}
.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0 15px;
  border-radius: 6px;
  color: var(--color-letra);
  background: var(--color-fondo);
}
.playlist {
  border-radius: 1rem;
  /*box-shadow: 1rem 0 100rem rgb(0 0 0 / 50%);*/
  padding: 0 30px 50px 30px;
}
.playlist h2 {
  padding: 30px 0 30px 0;
  text-align: center;
}
.playlist .song {
  color: var(--color-letra);
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
  text-transform: uppercase;
}
.playlist .song.playing {
  border-radius: 0.5rem;
  color: #0d6efd;
  background: var(--color-fondo);
}
@media (width: 915px) {
  html,
  body {
    background-size: 200% 200%;
    background-image: linear-gradient(
      to bottom right,
      #4affde 0%,
      #5b9dff 40%,
      #d06bff 60%,
      #ff34d2 100%
    );
    width: 100%;
    height: 150%;
    text-align: center;
    font-family: "Oswald", sans-serif;
    animation: moving 5s linear infinite alternate;
  }
}
</style>