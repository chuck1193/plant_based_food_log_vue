<template>
  <div class="food-log-edit">
    <ul>
      <li v-for="error in errors"> {{ error }}</li>
    </ul>
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <div>
          <label>Time of Day:</label>
          <select class="form-control" v-model="food_log.food_type">
            <option value="breakfast">Breakfast</option>
            <option value="lunch">Lunch</option>
            <option value="dinner">Dinner</option>
            <option value="snack">Snack</option>
          </select>
        </div>
        <div>
          Food: <input type="text" v-model="food_log.food">
          Calories <input type="text" v-model="food_log.calories">
          Quantity: <input type="text" v-model="food_log.quantity">
        </div>
        <div>
          <label>Workout:</label>
          <select class="form-control" v-model="food_log.workout">
            <option value="cardio">Cardio</option>
            <option value="gym">Gym</option>
            <option value="cycling">Cycling</option>
            <option value="aerobics">Aerobics/Dancing</option>
            <option value="yoga">Yoga</option>
            <option value=swimming>Swimming</option>
            <option value="team-sports">Team Sports</option> 
          </select>
        </div>
        <div>
          How much water have you had(in ounces)? <input v-model="food_log.water_intake">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
  var axios = require("axios");

  export default {
    data: function() {
      return {
        foodLog: {
          food_type: "",
          food: "",
          calories: "",
          quantity: "",
          workout: ""
        },
        errors: []
      };
    },
    created: function() {
      axios.get("/api/food_logs/" + this.$route.params.id)
      .then(response => {
        console.log(response.data);
        this.food_log = response.data;
      });
    },
    methods: {
      submit: function() {
        var params = {
          food_type: this.food_log.food_type,
          food: this.food_log.food,
          calories: this.food_log.calories,
          quantity: this.food_log.quantity,
          workout: this.food_log.workout
        };
        axios.patch("/api/food_logs/" + this.food_log.id, params)
          .then(response => {
            this.$router.push("/food_logs/" + this.food_log.id);
          }).catch(error => {
            this.errors = error.response.data.errors;
          });
      }
    }
  }
</script>