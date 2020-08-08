<template>
  <div class="signup">
    <div class="container">
      <form v-onn:submit.prevent="submit()">
        <h1>Signup</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>First Name:</label>
          <input type="text" class="form-control" v-model="firstName">
        </div>
        <div class="form-group">
          <label>Last Name:</label>
          <input type="text" class="form-control" v-model="lastName">
        </div>
        <div class="form-group">
          <label>Email:</label>
          <input type="text" class="form-control" v-model="email">
        </div>
        <div class="form-group">
          <label>Password:</label>
          <input type="text" class="form-control" v-model="password">
        </div>
        <div class="form-group">
          <label>Password Confirmation:</label>
          <input type="text" class="form-control" v-model="passwordConfirmation">
        </div>
        <div class="form-group">
          <label>Date of Birth:</label>
          <input type="text" class="form-control" v-model="dateOfBrith">
        </div>
        <div class="form-group">
          <label>Weight:</label>
          <input type="text" class="form-control" v-model="weight">
        </div>
        <div class="form-group">
          <label>Goal Weight:</label>
          <input type="text" class="form-control" v-model="goalWeight">
        </div>
        <div class="form-group">
          <label>Height:</label>
          <input type="text" class="form-control" v-model="height">
        </div>
        <div class="form-group">
          <label>Weekly Weight Loss Goal:</label>
          <input type="text" class="form-control" v-model="weeklyWeightLossGoal">
        </div>
        <div class="form-group">
          <label>Activity Level:</label>
          <input type="text" class="form-control" v-model="activityLevel">
        </div>
        <input type="submit" class="btn primary-btn" vale="Submit">
      </form>
    </div>
  </div>
</template>

<script>
  import axios from "axios"

  export default {
    data: function() {
      return {
        firstName: "",
        lastName: "",
        email: "",
        password: "",
        passwordConfirmation: "",
        dateOfBrith: "",
        weight: "",
        goalWeight: "",
        height: "",
        weeklyWeightLossGoal: "",
        activityLevel: "",

          errors: []
      };
    },
    methods: {
      submit: function() {
        var params = {
          first_name = this.firstName,
          last_name = this.lastName,
          email = this.email,
          password = this.password,
          password_confirmation = this.passwordConfirmation,
          date_of_birth = this.dateOfBrith,
          weight: this.weight,
          goal_weight = this.goalWeight,
          height = this.height,
          weekly_goal = this.weeklyWeightLossGoal,
          activity = this.activityLevel
        };
        axios
          .post("/api/users", params)
          .then(response => {
            this.$router.push("/login");
          })
          .catch(error => {
            this.errors = error.response.data.errors;
          });
      }
    }
  };
</script>