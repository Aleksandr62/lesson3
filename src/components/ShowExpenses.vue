<template>
  <div>
    <div class="total"> Total: {{ amount }} </div>   
    <table class="ShowExpenses">
      <tr class="header">
        <td class="cell">#</td>
        <td class="cell">Date</td>
        <td class="cell">Category</td>
        <td class="cell">Value</td>
      </tr>
      <tr v-for="(expense, idx) in dataExpensesPage" :key="idx">
        <td class="cell">{{ expense.id }}</td>
        <td class="cell">{{ dateToString(new Date(expense.date)) }}</td>
        <td class="cell">{{ expense.category }}</td>
        <td class="cell">{{ +expense.cost }}</td>
      </tr>
    </table>
    <pagination
      :quantityItems="quantityItems"
      :quantityOnPage="quantityOnPage"
      @select-page="showPage"
    />    
  </div>
</template>

<script>
import Pagination from '@/components/Pagination.vue';

export default {
    name: 'ShowExpenses',    
    props:  {
        expenses: {
            type: Array,
            default: () => [],
        },
    },
    components: {
        Pagination
    },
    data() {
        return {
            quantityOnPage: 5,
            start: 0,
            end: 0            
        }
    },
    computed: {
        dataExpensesPage() {
            return this.expenses.slice(this.start, this.end)
        },
        quantityItems() {
            return this.expenses.length
        },
        amount() {
            return this.expenses.reduce((sum, el) => sum += el.cost, 0 )
        }        
    },
    methods: {
        showPage({start, end}) {
            this.start = start;
            this.end = end;
        },
        dateToString(date) {
            return date.toLocaleString('ru-RU', { year: 'numeric', month: 'numeric', day: 'numeric' })
        }
    }
}
</script>

<style scoped>
.ShowExpenses {
  border-collapse: collapse;
  width: fit-content;
}
.total {
    padding: 8px 20px;
    font-weight: 800;
}
.header {
  font-weight: 800;
}
.cell {
  padding: 10px 24px;
  border-bottom: 1px solid #ebebeb;
}
</style>