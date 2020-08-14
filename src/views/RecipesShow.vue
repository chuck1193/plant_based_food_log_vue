<template>
  <div class="recipes-show">
    <h1 v:model="recipe.name">{{ recipe.name }}</h1>
    <h2 v:model="recipe.ingredient_amount">{{ recipe.ingredient_amount }}</h2>
    <h2 v:model="recipe.ingredients">{{ recipe.ingredients }}</h2>
    <h3 v:model="recipe.calories">{{ recipe.calories }}</h3>
    <p v:model="recipe.instructions">{{ recipe.instructions }}</p>
  </div>
</template>

<script>
var axios = require('axios')

export default {
  data: function () {
    return {
      recipe: {
        id: '',
        name: '',
        ingredients: '',
        ingredient_amount: '',
        instructions: ''
      },
      errors: []
    }
  },
  created: function () {
    axios.get('/api/recipes' + this.$route.params.id)
      .then(response => {
        this.recipe = response.data
      }).catch(error => {
        this.errors = error.response.data.errors
      })
  },
  methods: {
    destroyRecipe: function () {
      axios.delete('/api/recipes/' + this.recipe.id)
        .then(response => {
          console.log('Successfully Deleted', response.data)
          this.$router.push('/recipes')
        }).catch(error => {
          this.errors = error.response.data.errors
          console.log(this.errors)
        })
    }
  }
}
</script>
