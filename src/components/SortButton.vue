<template>
  <div class="button-container">
    <ElButton type="primary" @click="clickAll">All</ElButton>
    <ElButton type="success" @click="clickIncome">Income</ElButton>
    <ElButton type="danger" @click="clickOutcome">Outcome</ElButton>
  </div>
</template>

<script>
export default {
  name: "SortButton",
  methods: {
    clickAll() {
      this.$emit('clickAll')
    },
    clickIncome() {
      this.$emit('clickIncome')
    },
    clickOutcome() {
      this.$emit('clickOutcome')
    }
  }
}
</script>

<style scoped>
.button-container {
  margin-bottom: 10px;
}

</style>
