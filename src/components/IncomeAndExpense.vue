<template>
    <div>
        <table>
            <thead>
                <tr>
                    <th>
                        No.
                    </th>
                    <th>
                        Detail
                    </th>
                    <th>
                        Income
                    </th>
                    <th>
                        Expense
                    </th>
                    <th>
                        Date
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(info, index) in information" v-bind:key="index">
                    <td>{{ index + 1 }}</td>
                    <td>{{ info.activity }}</td>
                    <td>{{ info.income }}</td>
                    <td>{{ info.expense }}</td>
                    <td>{{ info.date }}</td>
                </tr>
            </tbody>
        </table>
        <br><br>
        <p>Sum of Total Value: {{ total }}</p>
    </div>
</template>

<script>
import IncomeAndExpenseStore from '@/store/IncomeAndExpenseStore'

export default {
    data(){
        return{
            information: [],
            total: 0
        }
    },
    created(){
        this.fetchInformation()
        this.$root.$refs.IncomeAndExpense = this

    },
    methods: {
        async fetchInformation(){
            await IncomeAndExpenseStore.dispatch('fetchInformation')
            this.information = IncomeAndExpenseStore.getters.Informations
            this.CalTotal()
        },
        CalTotal(){
            IncomeAndExpenseStore.dispatch('CalTotal', this.information)
            this.total = IncomeAndExpenseStore.getters.total
        }
    }
}
</script>

<style>
    table{
        width: 66%;
        margin-left: auto;
        margin-right: auto;
        margin-top: auto;
        border-bottom: 1px solid white;
    }
    th {
        border: 1px solid white
    }
    tr,td {
        border-right: 1px solid white;
        border-left: 1px solid white;
    }
    p {
        font-family: Helvetica, Arial,  sans-serif;
    }


</style>