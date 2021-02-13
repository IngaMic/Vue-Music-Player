<template>
    <div id="app">
        <header><h1>OST player</h1></header>
        <div class="image">
            <h2 class="song-title">
                {{ current.title }} <br />
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
                    @click="play(song)"
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
        //this.player.play();
    },
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body {
    background-color: #0e0a01;
    color: white;
    font-family: sans-serif;
}
header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: #212121;
    color: #fff;
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
.song-title {
    color: white;
    font-size: 32px;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
}
.song-title {
    padding-top: 100px;
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
    display: block;
    width: 100%;
    padding: 15px;
    font-size: 20px;
    font-weight: 700;
    cursor: pointer;
}
.playlist .song:hover {
    color: #fff;
}
.playlist .song.playing {
    color: #fff;
    border-radius: 10px;
    background-image: linear-gradient(
        to right,
        #e8ece5,
        #a6b5b8,
        #8390a0,
        #84a0a4
    );
}
.song {
    color: white;
}
</style>
