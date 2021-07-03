<template>
  <div>
    <div class="top">
      <form-add-expense @add-espense="addEspense" />      
    </div>
    <show-expenses :expenses="dataExpenses" />
  </div>
</template>

<script>
import FormAddExpense from '@/components/FormAddExpense.vue';
import ShowExpenses from '@/components/ShowExpenses.vue';

export default {
  name: 'App',
  data() {
    return {
      counterId: this.counter(),
      dataExpenses: [],
    }
  },
  components: {
    FormAddExpense,
    ShowExpenses
  },
  methods: {
    counter() {
      let count = 0;
      return () => count +=1;
    },
    fetch(data) {
      this.dataExpenses = data;
    },
    addEspense(item) {
      this.dataExpenses.push({...item, id: this.counterId()});
    },
  },
  created() {
    if(!this.dataExpenses.length)
    this.fetch([
      {id: this.counterId(), date: '2021-03-17', category: 'Еда', cost: 1000 },
      {id: this.counterId(), date: '2021-04-12', category: 'Одежда', cost: 4500 },     
      {id: this.counterId(), date: '2021-01-21', category: 'Еда', cost: 1000 },
      {id: this.counterId(), date: '2021-05-05', category: 'Одежда', cost: 4500 },      
      {id: this.counterId(), date: '2021-05-10', category: 'Еда', cost: 1000 },
      {id: this.counterId(), date: '2021-02-20', category: 'Одежда', cost: 4500 },                   
    ]);
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
