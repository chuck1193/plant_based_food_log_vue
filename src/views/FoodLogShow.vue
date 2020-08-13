<template>
  <div class="food-logs-show">
    <div v:for="foodLog in foodLogs">
      <h2>Date:</h2>
      <table>
        <thead></thead>
        <tbody>
          <tr>
            <th></th>
            <td v:model="foodLog.food_type">{{ foodLog.food_type }}</td>
            <td></td>
          </tr>
          <tr>
            <td v:model="foodLog.food">{{ foodLog.food }}</td>
            <td></td>
          </tr>
          <tr>
            <td v:model="foodLog.calories">{{ foodLog.calories }}</td>
            <td></td>
          </tr>
          <tr>
            <td v:model="foodLog.quantity">{{ foodLog.quantity }}</td>
            <td></td>
          </tr>
          <tr>
            <td></td>
            <td></td>
          </tr>
        </tbody>
      </table>
      <h3 v:model="foodLog.water_intake">Today's water intake: {{ food_log.water_intake }}</h3>
      <h4 v:model="foodLog.workout">{{ foodLog.workout }}</h4>
    </div>
  </div>
</template>

<script>
var axios = require('axios')

export default {
  data: function () {
    return {
      foodLog: {
        id: '',
        food_type: '',
        food: '',
        calories: '',
        quantity: '',
        workout: '',
        water_intake: ''
      },
      errors: []
    }
  },
  created: function () {
    axios.get('/api/food_logs' + this.$route.params.id)
      .then(response => {
        this.food_log = response.data
      }).catch(error => {
        this.errors = error.response.data.errors
      })
  },
  methods: {
    destroyFoodLog: function () {
      axios.delete('/api/food_logs/' + this.food_log.id)
        .then(response => {
          console.log('Successfully Deleted', response.data)
          this.$router.push('/food_logs')
        }).catch(error => {
          this.errors = error.response.data.errors
          console.log(this.errors)
        })
    }
  }
}
</script>
