<template>
  <div class="home">
    <h1>income and expenditure table</h1> 
    <income-and-expense></income-and-expense>
    <br>
    <add-activity></add-activity>
  </div>
</template>

<script>
import AddActivity from '../components/AddActivity.vue'
// @ is an alias to /src
import IncomeAndExpense from '../components/IncomeAndExpense.vue'


export default {
  name: 'Home',
  components: {
    IncomeAndExpense,
    AddActivity
  }
}
</script>

<style lang="scss" scoped>
  h1 {
    font-family: Helvetica, Arial,  sans-serif;
  }
</style>
