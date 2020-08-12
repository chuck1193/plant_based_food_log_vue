<template>
  <div class="recipes-new">
    <h1>New Recipe</h1>
    <ul>
      <li v-for="error in errors"> {{ error }}</li>
    </ul>
    <div class=" container">
      <form v-on:submit.prevent="submit()">
        <div>
          Name: <input v-model="newRecipeName">
        </div>
        <div>
          Amount of Ingredients: <input type="text" v-model="newRecipeIngredientsAmount">
          Ingredients: <input type="text" v-model="newRecipeIngredients">
        </div>
        <div>
          Instructions: <input type="text" v-model="newRecipeInstructions">
        </div>
        <input type="submit" value="Add" class="btn btn-primary">
      </form>
    </div>
  </div>
</template>

<script>
  var axios = require("axios");

  export default {
    data: function() {
      return {
        reciipes: [],
        newRecipeName: "",
        newRecipeIngredientsAmount: "",
        newRecipeIngredients: "",
        newRecipeInstructions: "",
        errors: []
      };
    },
    created: function() {}
      methods: {
        submit: function() {
          var params = {
            name: this.newRecipeName,
            ingredient_amount: this.newRecipeIngredientsAmount,
            ingredients: this.newRecipeIngredients,
            instructions: this.newRecipeInstructions
          };
          axios.post("/api/recipes/", params)
          .then(response => {
            console.log("Saved", repsonse.data);
            this.$router.push("/")
          }).catch(error => {
            this.errors = error.response.data.errors;
          });
        }
      }
  };
</script>