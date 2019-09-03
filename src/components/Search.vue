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
    keyWord: "",
    currentPage: 1
  }),
  methods: {
    searchKeyWord() {
      axios.get(`https://www.food2fork.com/api/search?key=f07c3692e6f94650d235ac50898e99c7&q=${this.keyWord}&page=${this.currentPage}`)
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
    background-color:#fff500;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .button:hover{
    background-color:#f92a75;
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
