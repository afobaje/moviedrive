<template>
    <div class="recipe">
        
        
        <div v-if="displayType=='grid'">
            <div class="suggestions">
            <h3>{{intro}}</h3>
            <input type="text" name="" id="" :placeholder="placeholder" @keyup.13="getSearch()" v-model="searchtext">
        </div>
            <div class="resultindex">
            <div class="results" v-for="(result,index) in results" :key="index.id" @click="getId(result)">
            <img :src="result.Poster" :alt="result.imdbID" >
            <p>{{result.Title}}</p>
            <p>{{result.Year}}</p>
            <a href="#" class="unid">{{Detailing}}</a>
            </div>
        
            </div>
        </div>
        <div v-else-if="displayType==='details'" class="details">
            
            <button id="backbutton" @click="displayType='grid'">Back</button>
            <div class="resultdetails">
                <img :src="searchIndex.Poster" :alt="searchIndex.Title">
                <div class="infotain">
                    <h2>{{searchIndex.Title}}</h2>
                <ul>
                <li>Year: {{searchIndex.Year}}</li>
                <li>Rated: {{searchIndex.Rated}}</li>
                <li>Released: {{searchIndex.Released}}</li>
                <li>Runtime: {{searchIndex.Runtime}}</li>
                <li>Genre: {{searchIndex.Genre}}</li>
                <li>Director: {{searchIndex.Director}}</li>
                <li>Writer: {{searchIndex.Writer}}</li>
                <li>Actors: {{searchIndex.Actors}}</li>
                <li>Language: {{searchIndex.Language}}</li>
                <li>Awards: {{searchIndex.Awards}}</li>
                <li>Country: {{searchIndex.Country}}</li>
                <ul>
                    
                    <li v-for="(rating,idc) in searchIndex.Ratings" :key="idc.id">{{rating.Source}} Rating: {{rating.Value}}</li>
                </ul>
                <li>IMDB Rating: {{searchIndex.imdbRating}}</li>
                <li>Metascore: {{searchIndex.Metascore}}</li>
                <li>IMDB Votes: {{searchIndex.imdbVotes}}</li>
                <li>IMDB ID: {{searchIndex.imdbID}}</li>
                </ul>                
                </div>
                
            </div>
            

        </div>
        <span v-if="baderr">
            {{baderr}}
        </span>

    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'recipe',
    data(){
        return{
            intro:'Search for any movie...',
            recipe:'',
            Detailing:'VIEW DETAILS',
            results:'',
            title:'',
            searchtext:'',
            placeholder:'Type movie title here',
            baderr:"",
            displayType:'grid',
            src:'',
            selectedItem:null,
            searchIndex:'',
            APIKEY: 'edd3b51',
            options:{
                method: 'GET',
                headers:{
                    'Accept':'application/json',
                    'Content-Type':'application/json;charset=UTF-8'
                }
            
            },
    
        }
    },
    
   
    methods:{
        
        getSearch(){
            axios.get(`https://www.omdbapi.com/?s=${this.searchtext}&apikey=${this.APIKEY}`)
            .then(response=>{
                this.value=response
                this.results=response.data.Search
               
                
            })
            .catch(err=>{
                
                this.baderr=err
            })
        },
        getId(result){
            this.displayType='details'
            
            this.selectedItem=result
            
            axios.get(`https://www.omdbapi.com/?i=${this.selectedItem.imdbID}&apikey=${this.APIKEY}`)
            .then(response=>{
                this.searchIndex=response.data
                
            })
        }
    }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins&family=Roboto&display=swap');
$input-color: #dbdbdb;
$button-color: #0095f6;
.recipe{
    margin-top: .5em;
    height: auto;
    font-family: 'Roboto', sans-serif;
    padding: 1em;
}
.suggestions{
    input[type="text"]{
        border-radius: 3px;
        height: 2em;
        outline: none;
        border-color: black;
        border: solid 1px $input-color;
    }
}
.resultindex{
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-gap: .5em;
    a{
        color: $button-color;
        text-decoration: none;
        cursor: pointer;
    }
    div{
        height: 24em;
        border-radius: 10px;
        width: 300px; 
        margin-top: 1em;
        transition: .5s ease-in-out;;
        &:hover,&:active{
            box-shadow: 0 0 8px black;
        }
        img{
            height: 18em;
            
            width: 300px;
            border-top-right-radius: 10px;
            border-top-left-radius: 10px;
            
        }
    }
}
@media screen and (max-width:992px){
    .resultindex{
    display: grid;
    grid-template-columns: repeat(2,1fr);
    grid-gap: .25em;
    a{
        color: $button-color;
        text-decoration: none;
        cursor: pointer;
    }
    div{
        height: 20em;
        border-radius: 10px;
        width: 300px; 
        //cursor: pointer;
        margin-top: 1em;
        transition: .5s ease-in-out;;
        &:hover,&:active{
            box-shadow: 0 0 8px black;
        }
        img{
            height: 15em;
            
            width: 300px;
            border-top-right-radius: 10px;
            border-top-left-radius: 10px;
            
        }
    }
}

}
@media screen and (max-width:600px){
    .resultindex{
    display: grid;
    grid-template-columns: 1fr;
    
    a{
        color: $button-color;
        text-decoration: none;
        cursor: pointer;
    }
    div{
        height: 20em;
        border-radius: 10px;
        width: 200px; 
        cursor: pointer;
        margin-top: 1em;
        transition: .5s ease-in-out;;
        &:hover,&:active{
            box-shadow: 0 0 8px black;
        }
        img{
            height: 15em;
            
            width: 230px;
            border-top-right-radius: 10px;
            border-top-left-radius: 10px;
            
        }
    }
 }

 .resultdetails{
    display: flex;
    margin-top: 1em;
   
    .infotain{
        
        text-align: left;
    }

    ul{
        list-style: none;
        padding: 0;
        margin: 0;
        li{
            margin-top: .5em;
        }
    }
 }
 #backbutton{
    position: relative;
    background-color: $button-color;
    left: -200px;
    top: 150px;
    margin-left: 5rem;
    border-radius: 6px;
    width: 6em;
    height: 2.5em;
    border: 1px solid $button-color;
    cursor: pointer;
    outline: none;
    
 }

}




#backbutton{
    position: relative;
    background-color: $button-color;
    margin-left: -70rem;
    border-radius: 6px;
    width: 6em;
    height: 2.5em;
    border: 1px solid $button-color;
    cursor: pointer;
    outline: none;
    
}
.resultdetails{
    display: grid;
    margin-top: 1em;
    grid-template-columns: repeat(3,1fr);
    .infotain{
        grid-column: 2/span 3;
        text-align: left;
    }

    ul{
        list-style: none;
        
        padding: 0;
        margin: 0;
        li{
            margin-top: .5em;
        }
    }
}
</style>