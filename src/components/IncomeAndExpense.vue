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
        {{ total }}
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
        border-bottom: 1px solid #000;
    }
    th {
        border: 1px solid black
    }
    tr,td {
        border-right: 1px solid black;
        border-left: 1px solid #000;
    }

</style>