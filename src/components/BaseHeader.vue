<template>
  <header>
      <input type="text" v-model="searchText">
      <select name="lang" id="" v-model="language">
        <option value="it">IT</option>
        <option value="de">DE</option>
        <option value="es">ES</option>
        <option value="fr">FR</option>   
      </select>
      <button @click="search">Search</button>
      <div v-if="movieResearch.length !== 0" class="container">
      <h2>Movies</h2>
           <div v-for="(movie, i) in movieResearch" :key="i" class="card">
           <h3>{{movie.title}}</h3>
           </div>
     </div>
     <div v-if="seriesTVRasearch.length !== 0" class="container">
     <h2>TV series</h2>
           <div v-for="(tv, i) in seriesTVRasearch" :key="i" class="card">
           <h3>{{tv.name}}</h3>
           </div>
     </div>
    <!-- @change="changeLanguage" -->
    
  </header>
    
</template>

<script>
import axios from 'axios'
export default {
  name: 'BaseHeader',
  data(){
    return{
        searchText: "",
        movieResearch: [],
        seriesTVRasearch: [],
        language: "",
        originalTitle: ""
    }
    },

    methods: {
        search(){
            axios.get("https://api.themoviedb.org/3/search/movie?api_key=5d9663769947e4847cbf4363c075f1a8", {
                params: {
                    original_language: this.language,
                    query: this.searchText,
                    
                }
            })
            .then(result =>{ 
                this.movieResearch = result.data.results;
            });

            axios.get("https://api.themoviedb.org/3/search/tv?api_key=5d9663769947e4847cbf4363c075f1a8", {
                params: {
                    original_language: this.language,
                    query: this.searchText,
                    
                }
            })
            .then(result =>{ 
                this.seriesTVRasearch = result.data.results;
            })

        }
    },
}


</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
    display: flex;
    flex-wrap: wrap;
    background-color: gray;

    h2 {
        width: 100%;
    }
}

.card {
    width: 150px;
    height: 300px;
    background-color: black;
    color: #fff;
}

</style>
