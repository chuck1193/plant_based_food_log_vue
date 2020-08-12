<template>
  <div class="container">
    <h1>Logs</h1>
    <div v-for="foodLog in foodLogs">
      <h2>{{ foodLog.food }}</h2>
      <p></p>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data: function() {
      return {
        user: [],
        foodLog: [],
      }
    }
  }
</script>