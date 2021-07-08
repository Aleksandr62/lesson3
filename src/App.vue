<template>
  <div>
    <div class="top">
      <form-add-expense
        :countExpenses="countExpenses"
        :categories="categories"
        @add-espense="addNewCost"
      />
      <form-add-category
        :categories="categories"
        @add-category="addNewCategory"
      />      
    </div>
    <show-expenses
      :expenses="expensesPage"
    />
    <pagination
      :quantityOnPage="quantityOnPage"
      :countPages="countPages"
      @select-page="fetchData"
    />
  </div>
</template>

<script>
import FormAddExpense from '@/components/FormAddExpense.vue';
import FormAddCategory from '@/components/FormAddCategory.vue';
import ShowExpenses from '@/components/ShowExpenses.vue';
import Pagination from '@/components/Pagination.vue';
import { mapActions } from 'vuex'

const expenses = [
            {id: 1, date: '2021-03-17', category: 'Food', cost: 1000 },
            {id: 2, date: '2021-04-12', category: 'Entertaiment', cost: 4500 },     
            {id: 3, date: '2021-01-21', category: 'Food', cost: 1000 },
            {id: 4, date: '2021-05-05', category: 'Education', cost: 4500 },      
            {id: 5, date: '2021-05-10', category: 'Sport', cost: 1000 },
            {id: 6, date: '2021-02-20', category: 'Navigation', cost: 4500 },                   
          ]
const category = ['Food', 'Entertaiment', 'Education', 'Sport', 'Navigation' ]

export default {
  name: 'App',
  data() {
    return {
      expensesPage: [],
      quantityOnPage: 5,
    }
  },
  components: {
    FormAddExpense,
    FormAddCategory,
    ShowExpenses,
    Pagination
  },
  computed: {
    countExpenses() {
      return this.$store.getters.count
    },
    countPages() {
      return Math.ceil(this.countExpenses / this.quantityOnPage)
    },
    categories() {
      return this.$store.getters.categories
    },
  },
  methods: {
    ...mapActions([
      'addData',
      'getAllExpenses' 
    ]),
    
    fetchData(page) {
      const count = this.quantityOnPage
      this.expensesPage = this.$store.getters.expenses.slice(page * count, page * count + count)
    },
    addNewCost(data) {
        this.$store.dispatch('addData', {...data, id: this.countExpenses + 1})  
    },
    addNewCategory(cat) {
        this.$store.commit('addNewCategory', cat)  
    }      
  },
  created() {
    this.getAllExpenses({expenses, category})
    this.fetchData(0)
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.top {
  display: flex;
}
</style>
