<template>
    <v-card>
      <v-card-title>
        <h2>Vue en détaille</h2>
        <strong>{{ data.title }}</strong>
        <v-spacer></v-spacer>
        <v-btn icon @click="$emit('close')">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" md="4">
                
              <v-img :src="'https://image.tmdb.org/t/p/w500'+data.poster_path" :alt="data.title" />
            </v-col>
            <v-col cols="12" md="8">
              <v-row>
                <v-col cols="12">


        <v-rating v-model="data.vote_average" precision="0.5" readonly></v-rating>
                </v-col>
                <v-col cols="12">
                  <v-chip v-if="data.release_date">{{ data.release_date }}</v-chip>
                </v-col>
                <v-col cols="12" v-if="data.genres && data.genres.length > 0">
                  <v-chip>{{ 
                  data.genres.map((item) => {
             return item.name;
           }).join(", ")
          }}</v-chip>
                </v-col>
                <v-col cols="12" v-if="data.production_companies && data.production_companies.length > 0">
                  <v-chip>{{ 
                      data.production_companies.map((item) => {
                        return item.name;
                      }).join(", ") 
                    }}
                    </v-chip>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
          <v-row>
  
            <v-col cols="12">
              <v-divider></v-divider>
            </v-col>
            <v-col cols="12">
              <p>Description</p>
              <p>{{ data.overview }}</p>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="$emit('close')">Close</v-btn>
      </v-card-actions>
    </v-card>
</template>
<script>
import axios from 'axios';
const conf = require('../config.json');
const apiKey = conf["api_key"]
export default {
    name: 'MovieDetail',
    data(){
        return{
            data : []
        }
    },
    props: {
        movieId : {
            type: Number,
            required: true
        }
    },
    beforeMount(){

            axios.get(conf["url"]['movie_detail']+this.movieId, {
                headers: {
                    'Authorization': `bearer ${apiKey}`
                }
            })
            .then((res)=>{
                this.data = res.data
                console.log(this.data.genres);
            })
            .catch((err)=>{
                console.log(err)

            })
        
    }

}

</script>