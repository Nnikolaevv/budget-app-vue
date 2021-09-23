<template>
  <ElCard :header="header">
    <SortButton @clickAll="onClickAll" @clickIncome="onClickIncome" @clickOutcome="clickOutcome"/>
    <template v-if="!isEmpty">
      <div class="list-item" :class="item.type === 'Income' ? { income: incomeHide } : { outcome: outcomeHide }"
           v-for="(item, prop) in list" :key="prop">
        <span class="budget-comment">{{ item.comment }}</span>
        <span class="budget-value" :class="item.type === 'Income' ? 'green' : 'red'">{{ item.value }}</span>
        <i v-if="isIncome(item.type)" class="el-icon-top"></i>
        <i v-else class="el-icon-bottom"></i>
        <ElButton type="danger" size="mini" @click="deleteItem(item.id)">Delete</ElButton>
      </div>
    </template>
    <ElAlert v-else type="info" :title="emptyTitle" :closable="false"/>
  </ElCard>
</template>

<script>
import SortButton from "@/components/SortButton";

export default {
  name: "BudgetListItem",
  components: {
    SortButton
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    centerDialogVisible: false,
    header: 'Budget List',
    emptyTitle: 'Empty LIst',
    incomeHide: false,
    outcomeHide: false
  }),
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id)
    },
    isIncome(type) {
      return type === 'Income'
    },
    onClickAll() {
      this.incomeHide = false;
      this.outcomeHide = false
    },
    onClickIncome() {
      this.incomeHide = false;
      this.outcomeHide = true
    },
    clickOutcome() {
      this.incomeHide = true;
      this.outcomeHide = false
    }
  },
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length
    },
  }
}
</script>

<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}

i {
  margin-right: 5px;
}

.green {
  color: green;
}

.red {
  color: red;
}

.income {
  display: none;
}

.outcome {
  display: none;
}

</style>
