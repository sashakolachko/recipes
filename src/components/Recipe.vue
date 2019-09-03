<template lang="html">
  <div class="recipe-container">
    <img  class="image" v-bind:src="imgUrl" :alt="title">
    <h3 class="title">{{ title }}</h3>
    <p class="p">Social rank: <span class="span"> {{ socialRank }} </span></p>
    <p class="p">Publisher: <span class="span"> {{ publisher }} </span></p>
    <a  class="link" :href="link">See more</a>
  </div>
</template>

<script>
export default {
  name: 'Recipe',
  props: {
    publisher: String,
    imgUrl: String,
    socialRank: Number,
    title: String,
    link: String
  }
}
</script>

<style lang="css" scoped>
  .recipe-container{
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    justify-content: space-around;

  }
  .image{
    width: 100%;
    height: 250px;
  }
  .title{
    text-align: center;
    margin:0;
    color:#ee1659;
  }
  .p{
    margin: 0;
  }
  .link{
    color:#000;
    margin-top: 0;
    cursor: pointer;
  }
  .link:hover{
    color:#ee1659;
  }
  .span{
    color:#ff3674;
  }
</style>
