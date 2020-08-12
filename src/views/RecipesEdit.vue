<template>
  <div recipe-edit>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <div>
          Name: <input type="text" v-model="recipe.name">
        </div>
        <div>
          Amount of Ingredient: <input v-model="recipe.ingredient_amount">
          Ingredients: <input type="text" v-model="recipe.ingredients">
        </div>
        <div>
          Instructions: <input v-model="recipe.instructions">
        </div>
        <input type="submit" value="Update" class="btn btn-primary">
      </form>
    </div>
  </div>
</template>

<script>
  var axios = require("axios");

  export default {
    data: function() {
      return {
        recipe: {
          name: "",
          ingredient_amount: "",
          ingredients: "",
          instructions: ""
        },
        errors: []
      };
    },
    created: function() {
      axios.get("/api/recipes/" + this.$route.params.id)
      .then(response => {
        console.log(response.data);
        this.recipe = response.data;
      });
    },
    methods: {
      submit: function() {
        var params = {
          name: this.recipe.name,
          ingredient_amount: this.recipe.ingredient_amount,
          ingredients: this.recipe.ingredients,
          instructions: this.recipe.instructions
        };
        axios.patch("/api/recipes/" + this.recipes.id, params)
        .then(response => {
          this.$router.push("/recipes/" + this.recipes.id);
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
      }
    }
  }
</script>