<template>
    <div>
        <button @click="changePage('home')">
        Go back to home
        </button>

        <div v-if="!endOfGame">
            <Carousel 
            :songs="songs"
            :activeSongIndex="activeSongIndex"

            @change-song-index="changeActiveSongIndex"
            />

            <div v-for="(vote, index) in votes" :key="index">
                <button v-if="!vote.isVoted" @click="sendVote(vote.points)">
                    Add {{vote.points}}
                </button>
            </div>
        </div>

        <div v-if="endOfGame">
            You voted everything
        </div>
    </div>
</template>

<script>
import Carousel from "../components/Carousel.vue";
export default {
    name: "PageGame",
    components:{
        Carousel
    },
    methods: {
        changePage(page){
            this.$emit("change-page", page);
        },
        changeActiveSongIndex(index) {
            this.activeSongIndex = index;
        },

        sendVote(points) {
            // hidding the vote button
            this.votes.map((vote) => {
                if (vote.points == points) {
                    vote.isVoted = true;
                }
            })

            // post vote to the api
            const song = this.songs[this.activeSongIndex];

            fetch("https://localhost:5001/Votes", {
                method: "POST",
                headers: {
                    'Accept': 'application/json, text/plain',
                    'Content-Type': 'application/json;charset=UTF-8'
                },
                body: JSON.stringify({
                    songID: song.id,
                    points: points
                })
            }).then((response) => {
                return response.json()
            }).then((answer) => {
                console.log(answer);
            });
            const activeVotes = this.votes.filter((vote) => !vote.isVoted);
            // check the game is done
            if (activeVotes.length == 0) {
                this.endOfGame = true;
            }
        },
        fetchSongs() {
            const url = "https://localhost:5001/Songs";
            fetch(url)
                .then((response) => response.json())
                .then((songs) => {
                this.mapArtistOnSongs(songs);
            });
        },
        mapArtistOnSongs(songs) {
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
        }
    },
    data(){
        return{
            songs: [],
            activeSongIndex: 0,
            endOfGame: false,
            votes: [
                {
                    points: 1,
                    isVoted: false
                },
                {
                    points: 2,
                    isVoted: false
                },
                {
                    points: 4,
                    isVoted: false
                },
                {
                    points: 8,
                    isVoted: false
                },
            ]
        }
    },
    mounted(){
        this.fetchSongs();
    }
}
</script>

