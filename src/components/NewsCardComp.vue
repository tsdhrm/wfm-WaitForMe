<template>
  <div class="flex flex-col w-screen">
    <div class="items-center justify-center flex flex-row uppercase tracking-widest font-bold mb-3 text-gray-400">Randomly-picked News</div>
    <div class="relative flex flex-row h-full">
      <!-- <img class="rounded-md brightness-50" src="../assets/card-bg.jpg"> -->
      <img class="rounded-md object-cover brightness-50" :src="selectedArticles.urlToImage">
      <div class="absolute px-6 py-4">
        <h4 class="text-xl font-semibold tracking-normal leading-normal text-white">
          {{selectedArticles.title}}
        </h4>
        <p class="text-sm text-gray-300 mb-5">
          {{selectedArticles.source}}
        </p>
        <p class="text-sm text-gray-300 mb-5">
          {{selectedArticles.content}}
        </p>
      </div>
      
    </div>
  </div>
</template>

  <script>
  export default {
    data() {
      return {
        selectedArticles:[],
        apiKey: "939ed328094444b7a66c71211b00082a",
        responseAvailable: false,
      }
    },
    mounted() {
      this.fetchNews();
    },
    methods: {
      fetchNews:function(){
        let requestOptions = {
          method: 'GET',
          redirect: 'follow'
        };
        let idx = Math.floor(Math.random()*11);
        fetch("https://newsapi.org/v2/top-headlines?country=id&apiKey=939ed328094444b7a66c71211b00082a", requestOptions)
        .then(response => response.json())
        .then(jsondata => this.selectedArticles = jsondata.articles[idx])
        .then(result => console.log(result))
        .catch(error => console.log('error', error));
      }
    },
  }
  </script>

<style>
  
</style>
