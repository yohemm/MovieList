<template>
    <h1>movieList</h1>
    <v-container>
      <v-row>
        <v-col v-for="film in moviesList" :key="film.id" cols="12" sm="6" md="4" lg="3">
          <v-card>
              <v-card-title><strong>{{ film.title }}</strong> - {{ film.release_date }}</v-card-title>
              <v-img :src="'https://image.tmdb.org/t/p/w500'+film.poster_path" :alt="film.title"></v-img>
            <!-- Bouton pour afficher les détails -->
                    <v-btn @click="this.$emit('open', film.id)">Plus d'information</v-btn>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
</template>
<script>
import axios from 'axios';
const conf = require('../config.json');
const apiKey = conf["api_key"]
console.log(apiKey)
console.log(conf["url"]['movie_list'])
export default {
    name: 'MoviesList',
    data(){
        return{
            moviesList:[]
        }
    },
    mounted(){
        axios.get(conf["url"]['movie_list'], {
            headers: {
                'Authorization': `bearer ${apiKey}`
            }
        })
        .then((res)=>{
            console.log("GG")
            console.log(res)
            this.moviesList = res.data.results;
            console.log("Movie list")
            console.log(this.moviesList)
        })
        .catch((err)=>{
            console.log("perdu")
            console.log(err)

        })
    }
}
</script>