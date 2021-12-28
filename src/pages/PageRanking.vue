<template>
    <div>
        <button @click="changePage('home')">
            Back
        </button>
        <div v-for="(song,index) in songs" :key="index">
            {{ song.artist.name }} - {{ song.title }} - {{song.votes}}
        </div>
    </div>
</template>

<script>
export default {
    name: "PageRanking",
    methods: {
        changePage(page){
            this.$emit("change-page", page);
        },
        fetchSongs() {
            const url = "https://localhost:5001/Songs";
            fetch(url)
                .then((response) => response.json())
                .then((songs) => {
                    this.mapArtistsOnSongs(songs);
                    });
        },
        mapArtistsOnSongs(songs) {
            const url = "https://localhost:5001/Artists";
            fetch(url)
                .then((response) => response.json())
                .then((artists) => {
                // overwrite the existing array
                    songs.map((song) => {
                        const artistId = song.artistID; //3
                        // find the proper artist
                        const artist = artists.find(artist => artist.id == artistId);
                        // overwrite artist with the object
                        song.artist = artist;
                        return song;
                    });
                // overwrite the internal data
                    this.songs = songs;
                });
        }, 
        mapVotesOnSongs(songs){
            const url = "https://localhost:5001/Votes";
            fetch(url)
                .then((response) => response.json())
                .then((voteArray) => {
                    songs.map((song) => {
                        const songId = song.id;
                        const foundVotes = voteArray.filter((vote) => vote.songID == songId);
                        const totalVotes = foundVotes.map(item=>item.points).reduce((prev, next) => prev+next);
                        song.votes = totalVotes;
                        console.log(totalVotes);
                        return song;
                    });
                    this.songs = songs;
                });
        }
    },
    data(){
        return{
            songs: []
        }
    },
    mounted(){
        this.fetchSongs();
    }
}
</script>

