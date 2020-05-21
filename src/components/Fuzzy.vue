
<template>
    <div id="app">
    <h2>Books Fuzzy Search Application</h2>
    <div id="search_box"> <label>Search A Book </label> <input type="text" v-model="search"></div>
  <div id="results_container">
    <div class="single_book_detail" v-for="(item, index) in result" :key=index>
      <b> {{ item.title }}  </b><br/>
      <span> Author : {{ item.author.firstName +' '+item.author.lastName }} </span>
    </div>
  </div>
</div>
</template>
<script>

//import Vue from 'vue/dist/vue.common.js'
import Fuse from 'fuse.js';
//import json from './listofbooks.json'



export default {
  name: "App",
  data() {
    return {
      search:'',
      fuse: null,
      /////////////////////
      list:[]
       ,
      /////////////////////////////
      result:[]
    };
  },
   
   async created()
   {
     
   }
   ,
   async mounted() {

 
  const response = await fetch('listofbooks.json')
  const Data = await response.json()
  this.list = Data
 
    var options = {
      shouldSort: true,
      threshold: 0.6,
      location: 0,
      distance: 100,
      maxPatternLength: 32,
      minMatchCharLength: 1,
      keys: [
        "title",
        "author.firstName"
      ]
    };
    
    this.fuse = new Fuse(this.list, options);
    this.result = this.list
  },
  watch: {
    
          search() {
           
           if (this.search.trim() === '')
             this.result = this.list
           else
             this.result = this.fuse.search(this.search.trim())
          
          }
  
  },
  methods: {
     getBooksData() {
          fetch("listofbooks.json")
           .then(response => response.json())
           .then(data => (this.list = data));
    
    }
  }
};


   
</script>

<style>

 #app {
 margin-top: 0px !important;
 }

  body {
    font-family: 'Ubuntu Mono', monospace;
    background-color: #f4eee9;
  }

  #search_box
  {
    background: mediumturquoise;
    padding: 12px;
  }

   #search_box label{
    color: black;
    font-size: 19px;
    text-transform: capitalize;
    margin-right: 22px;
}
.single_book_detail {
    background: #8d5a82;
    color: white;
    margin: 3px;
    padding: 4px;
    border-radius: 5px;
    /* width: 271px; */
    float: left;
}

#search_box  input[type="text"]{
    border: 2px solid;
    border-radius: 6px;
    height: 18px;
    width: 300px;
    padding: 10px;
    font-size: 20px;
    color: black;
}

span {
    font-size: 12px;
    font-style: italic;
    color: #c3f6ff;
}

</style>