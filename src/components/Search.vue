<template lang="html">
  <div class="container">
    <form class="search-form">
      <input v-model="keyWord" class="input" type="text" placeholder="Type an Ingredient or Name">
      <button @click="searchKeyWord()"  class="button" type="button">Search</button>
    </form>
    <div class="recipes">
      <div class="recipes__item" v-for="recipe in recipes">
        <Recipe
          :publisher="recipe.publisher"
          :imgUrl="recipe.imgUrl"
          :socialRank="recipe.socialRank"
          :title="recipe.title"
          :link="recipe.link"
        />
      </div>
    </div>

    </div>
</template>

<script>
import axios from 'axios';
import Recipe from './Recipe.vue';

export default {
  name: 'Search',
  components: {
    Recipe
  },
  data: () => ({
    recipes: [],
    keyWord: ""
  }),
  methods: {
    searchKeyWord() {
      axios.get(`https://www.food2fork.com/api/search?key=29c2b83abcb7c2b46aa5fe2f796fd3ec&q=${this.keyWord}`)
        .then(response => response.data.recipes.map(item => {
          this.recipes.push({
            publisher: item.publisher,
            imgUrl: item.image_url,
            socialRank: parseInt(item.social_rank),
            title: item.title,
            link: item.f2f_url
          })
        }));
    }
  }
}
</script>

<style lang="css" scoped>
  .container{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 80vw;
  }
  .search-form{
    display: flex;
    justify-content: space-between;
    width: 40%;
    height: 40px;
  }
  .input{
    width: 60%;
    box-sizing: border-box;
    padding: 7px;
    font-size: 15px;
  }
  .button{
    width: 30%;
    background-color:#f92a75;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .button:hover{
    color:#fff;
  }
  .recipes{
    margin-top: 40px;
    width: 80vw;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .recipes__item{
    width: 300px;
    height: 500px;
    margin-top: 20px;
  }
</style>
