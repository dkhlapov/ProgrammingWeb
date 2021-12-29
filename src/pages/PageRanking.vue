<template>
    <div>
        <button @click="changePage('home')">
            Back
        </button>
        <ol>
          <li v-for="song in sorted" :key="song.id">{{song.artist.name}} - {{ song.title }}: {{ song.votes }} votes</li>
        </ol>
    </div>
</template>

<script>
export default {
    name: "PageRanking",
    data(){
        return{
            songs: []
        }
    },
    mounted(){
        this.fetchSongs();
    },
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
        mapArtistsOnSongs(data) {
            const url1 = "https://localhost:5001/Artists";
            fetch(url1)
                .then((response) => response.json())
                .then((artists) => {
                    // overwrite the existing array
                    data.map((song) => {
                        const artistId = song.artistID; //3
                        // find the proper artist
                        const artist = artists.find(artist => artist.id == artistId);
                        // overwrite artist with the object
                        song.artist = artist;
                        return song;
                    });

                    // overwrite the internal data
                    this.mapVotesOnSongs(data);
                });
        }, 
        mapVotesOnSongs(data){
            const url = "https://localhost:5001/Votes";
            fetch(url)
                .then((response) => response.json())
                .then((voteArray) => {
                    data.map((song) => {
                        const songId = song.id;
                        const foundVotes = voteArray.filter((vote) => vote.songID == songId);
                        const totalVotes = foundVotes.map(item=>item.points).reduce((prev, next) => prev+next);
                        song.votes = totalVotes;
                        return song;
                    });
                    data.sort
                    this.songs = data;
                });
        }
    },
    computed:{
        sorted(){
            return this.songs.sort((a,b) => b.votes-a.votes);
        }
    }
    
}
</script>

