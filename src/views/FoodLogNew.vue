<template>
  <div class="food-log-new">
    <h1>New Log</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <div>
          Time of Day: <input v-model="newFoodLogTimeOfDay">
        </div>
        <div>
          Food: <input v-model="newFoodLogFood">
        </div>
        <div>
          Calories: <input v-model="newFoodLogCalories">
        </div>
        <div>
          Quantity: <input v-model="newFoodLogQuantity">
        </div>
        <div>
          Workout: <input v-model="newFoodLogWorkout">
        </div>
        <div>
          How much water have you had(in ounces)? <input v-model="newFoodLogWaterIntake">
        </div>
        <input type="submit" value="Submit" name="btn btn-success">
      </form>
    </div>
  </div>
</template>

<script>
  import axios = require("axios");

  export default {
    data: function() {
      return {
        foodLog: [],
        newFoodLogTimeOfDay: "",
        newFoodLogFood: "",
        newFoodLogCalories: "",
        newFoodLogQuantity: "",
        newFoodLogWorkout: "",
        newFoodLogWaterIntake: "",
        errors: []
      };
    },
created: function() {},
  methods: {
    submit: function() {
      console.log("Log submitted")
      var params = {
        food_type: this.newFoodLogTimeOfDay,
        food: this.newFoodLogFood,
        calories: this.newFoodLogCalories,
        quantity: this.newFoodLogQuantity,
        workout: this.newFoodLogWorkout,
        water_intake: this.newFoodLogWaterIntake
      };
      axios.post("/api/food_logs", params)
        .then(response => {
          console.log("Logged", response.data)
          this.$router.push("/")
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
      }
    }
  };
</script>