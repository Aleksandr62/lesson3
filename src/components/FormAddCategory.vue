<template>
  <div>
    <div v-if="showForm" class="filter" @click="showForm = !showForm"></div>
    <div class="wrapper-Form">
      <button class="addCost" @click="showForm = !showForm">
        Add new category +
      </button>
      <form
        v-if="showForm"
        class="addFormCoast"
        @submit.prevent.stop="$emit('add-category', category)"
      >
        <div class="row">
          <label for="category">Category:</label>
          <input
            v-model="category"
            class="inputData"
            id="category"
            type="text"
          />
        </div>
        <div class="row">
          <button class="btn-save" type="submit">Добавить</button>
          <button class="btn-close" @click="showForm = false">Закрыть</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
    props:  {
        categories: {
            type: Array,
            default: () => [],
        }
    },
    name: 'FormAddCategory',
    data(){
        return{
            showForm: false,
            category: ''
        }
    },
}
</script>

<style scoped>
.wrapper-Form {
  margin-left: 10px;
  width: fit-content;
  position: relative;
}
.addCost {
  padding: 10px 24px;
  color: white;
  background: teal;
  border: transparent;
  border-radius: 2px;
}
.filter {
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  position: absolute;
  background: hsla(210, 10%, 10%, 0.7);
  z-index: 10;
}
.addFormCoast {
  padding: 20px 40px;
  position: absolute;
  display: flex;
  flex-direction: column;
  border: 1px solid rgb(2, 136, 136);
  background: white;

  top: 0;
  left: calc(100% + 2px);
  z-index: 20;
}
.row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
}
.row:not(:last-child) {
  margin-bottom: 12px;
}
label {
  margin-right: 12px;
}
.inputData {
  padding: 8px 16px;
  border: none;
  border-bottom: 1px solid #2b2b2b;
  background: rgb(199, 198, 198);
  outline: none;
}
.inputData:focus {
  border-bottom: 1px solid #016401;
}
.btn-save,
.btn-close {
  margin-top: 8px;
  padding: 8px 16px;
  justify-self: end;
  border: transparent;
  background: teal;
  color: white;
  font-weight: 700;
  text-transform: uppercase;
}
.btn-close {
  background: rosybrown;
}
</style>