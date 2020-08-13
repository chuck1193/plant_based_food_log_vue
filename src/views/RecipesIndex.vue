<template>
  <div class="recipes-index">
    <div v-for="recipe in recipes">
      <h1>{{ recipe.name }}</h1>
      <h4>{{ recipe.ingredients }}</h4>
    </div>
  </div>
</template>

<script>
var axios = require('axios')

export default {
  data: function () {
    return {
      user: [],
      currentRecipes: {},
      recipes: []
    }
  },
  created: function () {
    axios.get('/api/recipes').then(response => {
      this.recipes = response.data
    })
  },
  methods: {}
}
</script>
