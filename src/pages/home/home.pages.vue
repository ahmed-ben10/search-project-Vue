<template>
    <main id="home">
        <header>
            <div id="titel-container">
                <h4 id="titel">Watch list</h4>
            </div>
            <Searchbar @searched="setSearchText"/>
        </header>
        <ListBox 
            v-for="(movie,key) in filteredMovie" 
            :key="key" 
            :movies="movie"
        />
        <footer>
            <p v-if="searchText!='' "> Gevonden resultaten: {{filteredMovie.length}}/{{movies.length}}</p>
        </footer>
    </main>
</template>

<script>
import Api from '@/api/api.js';
import Searchbar from '@/components/search-bar.component';
import ListBox from './components/list-box.component';
export default {
    name:"home",
    components:{
        Searchbar,
        ListBox
    },
    data:()=>{
        return {
            searchText: '',
            movies: []
        }
    },
    async created(){
        this.movies = await Api.Movie.fetchAll();
    },
    methods:{
        setSearchText(value){
            this.searchText = value;
        }
    },
    computed:{
        filteredMovie:function(){
            return this.movies.filter((movie) => {
                const title = movie.title.toLowerCase();
                const search = this.searchText.toLowerCase().trim();
                return title.includes(search);
            });
        }
    }
}
</script>

<style>
    #home{
        width: 50%;
        margin-left: 25%;
        margin-right: 25%;
    }

    #watch-list-container{
        background-color: #2c3e50;
        padding: 10px;
        border-radius: 5px;
        width: 100%;
        margin-bottom: 1%; 
    }



    #titel{
        color: #2c3e50; 
        font-weight: 900;
        background-color: #63b9db;
        padding: 10px;
        width: 100%;
        border-radius: 5px;
    } 



    #search-bar{
        padding: 5px;
        border-radius: 0px 5px 5px 0px;
        border-color: #63b9db;
        border: 1px solid #63B9DB;
        margin-bottom: 1%;
    }

    #search-label{
        border: solid #63B9DB;
        border-radius: 5px 0px 0px 5px;
        background-color: #63b9db;
        padding: 4px;
    }

    .already-watched{
        background-color: red !important;
    }

    #watch-list{
       list-style-type: none;
       background-color: #63B9DB;  
       padding: 10px;
       border-radius: 5px; 
    }

</style>
