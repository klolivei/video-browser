<template>
    <div>
        <SearchBar @termChange="display"></SearchBar>
        <VideoList :videos="videos"></VideoList>
        {{videos.length }}
    </div>
    
    
</template>

<script>
import SearchBar from "./components/SearchBar"
import VideoList from "./components/VideoList"
import axios from "axios"

const API_KEY = "AIzaSyClKANzuCQSX3TgixX1PwGXUZjjjjoHt0o"
export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList
    },
    data(){
        return {
            videos: []
        }
    },
    methods: {
        display(searchTerm){
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm
                }
            }).then(response => {
                this.videos = response.data.items
            })
        }
    }
}
</script>

<style lang="scss" scoped>

</style>