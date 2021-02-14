<template>
    <div id="app">
        <header>
            <h1>OST</h1>

            <span>player</span>
        </header>

        <div class="image">
            <div class="overlay"></div>
            <h2 class="song-title">
                [ {{ current.title }} ]<br />
                <span> {{ current.artist }} </span>
            </h2>
        </div>
        <main>
            <section class="player">
                <div class="controls">
                    <button class="prev" @click="prev">
                        <img src="./assets/prev.svg" height="25px" />
                    </button>
                    <button class="play" v-if="!isPlaying" @click="play">
                        <img src="./assets/play.svg" height="45px" />
                    </button>
                    <button class="pause" v-else @click="pause">
                        <img src="./assets/pause.svg" height="45px" />
                    </button>
                    <button class="next" @click="next">
                        <img src="./assets/next.svg" height="25px" />
                    </button>
                </div>
            </section>
            <section class="playlist">
                <h3>Playlist</h3>
                <button
                    v-for="song in songs"
                    :key="song.src"
                    @click="play(song), timestamp()"
                    :class="song.src == current.src ? 'song playing' : 'song'"
                >
                    {{ song.title }} - {{ song.artist }}
                </button>
            </section>
        </main>
    </div>
</template>

<script>
export default {
    name: "App",
    data() {
        return {
            current: {},
            index: 0,
            isPlaying: false,
            songs: [
                {
                    title: "Clouds on Arran",
                    artist: "Uplawmoor",
                    src: require("../src/assets/scandydrama1.wav"),
                },
                {
                    title: "Scandi crime Theme",
                    artist: "Uplawmoor",
                    src: require("../src/assets/scandydrama3.mp3"),
                },
                {
                    title: "At the Farm Road",
                    artist: "Uplawmoor",
                    src: require("../src/assets/scandydrama2.wav"),
                },
            ],
            player: new Audio(),
        };
    },

    methods: {
        play(song) {
            if (typeof song.src != "undefined") {
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
        prev() {
            this.index--;
            if (this.index < 0) {
                this.index = this.songs.length - 1;
            }
            this.current = this.songs[this.index];
            this.play(this.current);
        },
        next() {
            this.index++;
            if (this.index > this.songs.length - 1) {
                this.index = 0;
            }
            this.current = this.songs[this.index];
            this.play(this.current);
        },
    },
    created() {
        this.current = this.songs[this.index];
        this.player.src = this.current.src;
    },
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Bebas Neue", cursive;
}
body {
    background-color: #0e0a01;
    color: white;
    font-family: sans-serif;
}
header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: #212121;
    color: #fff;
}
h1 {
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
        "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
    border-bottom: 1px solid white;
}
span {
    letter-spacing: 5px;
    padding-top: 0px;
    font-size: 18px;
}
main {
    width: 100%;
    max-width: 768px;
    margin: 0 auto;
    padding: 25px;
}
.image {
    position: relative;
    z-index: -2;
    background-image: url("https://images.pexels.com/photos/1801/rocks-fog-path-foggy.jpg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940");
    height: 55vh;
    min-width: 100vw;
}
.overlay {
    position: absolute;
    z-index: 1;
    height: 100%;
    width: 100%;
    background: linear-gradient(rgba(0, 0, 0, 0.575), rgba(255, 255, 255, 0));
}
.song-title {
    position: relative;
    z-index: 2;
    color: rgb(214, 184, 16);
    padding-top: 100px;
    text-shadow: 2px 2px rgba(0, 0, 0, 0.301);
    font-size: 2.1rem;
    font-weight: 900;
    text-transform: uppercase;
    text-align: center;
}
.song-title span {
    font-weight: 400;
    font-style: italic;
}
.controls {
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
.play,
.pause {
    padding: 15px 25px;
    margin: 0px 15px;
}
.next,
.prev {
    margin: 0px 15px;
}
.playlist {
    padding: 0px 30px;
}
.playlist h3 {
    color: #d3dadc;
    font-size: 20px;
    font-weight: 400;
    margin-bottom: 30px;
    text-align: center;
}
.playlist .song {
    letter-spacing: 2.5px;
    display: block;
    color: whitesmoke;
    width: 100%;
    padding: 15px;
    font-size: 20px;
    font-weight: 700;
    cursor: pointer;
}
.playlist .song:hover {
    color: rgb(255, 252, 206);
}
.playlist .song.playing {
    color: rgb(214, 184, 16);
    border-radius: 10px;
    border: 1px solid rgba(255, 255, 255, 0.63);
}
.song {
    color: white;
}
</style>
