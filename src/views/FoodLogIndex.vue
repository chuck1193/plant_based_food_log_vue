<template>
  <div class="container">
    <h1>Logs</h1>
    <div v-for="foodLog in foodLogs">
      <h2>{{ foodLog.food_type }}: {{foodLog.food}}</h2>
      <h3>{{ foodLog.calories }}</h3>
      <h3>{{ foodLog.water_intake}}</h3>
      <p></p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data: function () {
    return {
      user: [],
      currentFoodLog: {},
      foodLog: []
    }
  },
  created: function () {
    axios.get('/api/food_logs').then(response => {
      this.foodLogs = response.data
    })
  },
  methods: {}
}
</script>
