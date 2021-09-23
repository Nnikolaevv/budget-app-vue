<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance" :class="colorAtTotalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";


export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: 'Income',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'Outcome',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      },
    },
  }),
  methods: {
    onDeleteItem(id) {
      if (!confirm('Delete?')) {
        return
      }
      this.$delete(this.list, id)
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      }
      const valuesOfObj = String(newObj.value)

      if (newObj.type === 'Outcome' && !valuesOfObj.includes('-')) {
        newObj.value = -(newObj.value)
      }
      this.$set(this.list, newObj.id, newObj)
    },

  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0)
    },
    colorAtTotalBalance() {
      if (this.totalBalance > 0) {
        return 'green'
      }
      if (this.totalBalance === 0) {
        return 'black'
      }
      return "red"
    }
  },
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


</style>
