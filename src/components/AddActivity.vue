<template>
  <div>
      <div>
          <div v-if="incomeIndex === 1">
              <label for="name">Activity</label>
              <input type="text" v-model="form.activity">
              <label class="income" id="e" for="name_jp">Income</label>
              <input type="text" v-model="form.income">
              <label for="type">Date</label>
              <input type="date" v-model="form.date">
              <button @click="addInfo">Add</button>
              <button @click="closeForm()">Cancel</button>
          </div>
          <div v-if="incomeIndex === 0">
              <label for="name">Activity</label>
              <input type="text" v-model="form.activity">
              <label class="expense" for="name_jp">Expense</label>
              <input type="text" v-model="form.expense">
              <label for="type">Date</label>
              <input type="date" id="e" v-model="form.date">
              <button @click="addInfo()">Add</button>
              <button @click="closeForm()">Cancel</button>
          </div>
          <div v-if="incomeIndex === -1">
            <button @click="openIncome">Add Income</button>
            <button @click="openExpense">Add Expense</button>
          </div>

      </div>
  </div>
</template>

<script>
import IncomeAndExpenseStore from "@/store/IncomeAndExpenseStore"
export default {
    data() {
        return {
            information: [],
            form: {
                activity: "",
                income: "",
                expense: "",
                date: "",
            },
            incomeIndex: -1
        }
    },
    created(){
        this.fetchInformation()
    },
    methods: {
        async fetchInformation(){
            await IncomeAndExpenseStore.dispatch('fetchInformation')
            this.information = IncomeAndExpenseStore.getters.Informations
        },
        addInfo() {
            let payload = {
                activity: this.form.activity,
                income: parseInt(this.form.income),
                expense: parseInt(this.form.expense),
                date: (this.form.date),
            }
            if (this.incomeIndex == 0)
            {
                payload.income = 0
            }
            else{
                payload.expense = 0
            }
            if (this.form.activity !== "" && this.form.date !== "" && (this.form.income !== this.form.expense))
            {
                IncomeAndExpenseStore.dispatch('addInfo',payload)
                this.closeForm()
                this.$root.$refs.IncomeAndExpense.CalTotal()
            }

        },
        openIncome()
        {
            this.incomeIndex = 1
        },
        openExpense()
        {
            this.incomeIndex = 0
        },
        closeForm()
        {
            this.incomeIndex = -1
            this.form = {
                activity: "",
                income: "",
                expense: "",
                date: "",
            }
        },        
    }
    
}
</script>

<style scoped lang="scss">
    input {
        margin-left: 10px;
        margin-right: 10px;
    }
    .income {
        color: green;
    }
    .expense {
        color: red;
    }
    button
    {
        margin: 0px 10px;
    }

</style>