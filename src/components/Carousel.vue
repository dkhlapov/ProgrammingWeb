<template>
    <div>
        <button @click="changeSong(-1)">
            Prev song
        </button>
        <div v-for="(song, index) in songs" :key="song.id">
            <div v-if="index == activeSongIndex">
                {{ song.artist.name }} - {{ song.title }}
            </div>
        </div>
        <button @click="changeSong(1)">
            Next song
        </button>
    </div>
</template>

<script>
    export default {
        name: "Carousel",
        props: [
            "songs",
            "activeSongIndex"
        ],
        methods: {
            changeSong(value) {
                let index = this.activeSongIndex;

                index += value;

                if (index < 0 ) {
                    index = this.songs.length - 1;
                }

                if (index == this.songs.length) {
                    index = 0;
                }

                this.$emit("change-song-index", index);
            }
        }
    }
</script>