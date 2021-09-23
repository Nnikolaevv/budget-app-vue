<template>
  <ElCard class="form-card">
    <ElForm :model="formData" ref="addItemForm" :rules="rules" lable-position="top">
      <ElFormItem label="Type" prop="type">
        <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
          <ElOption lable="Income" value="Income"></ElOption>
          <ElOption lable="Outcome" value="Outcome"></ElOption>
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comment" prop="comment">
        <ElInput v-model="formData.comment"></ElInput>
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value"></ElInput>
      </ElFormItem>
      <ElButton @click="onSubmit" type="primary">Submit</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  name: "Form",
  data() {
    const foo = function (rule, value, callback) {  //Custom rules, function form
      if (value < 10) {
        callback(new Error("Value must be more 10")); //Write the error message here
      } else {
        callback();
      }
    }
    return {
      formData: {
        type: 'Income',
        comment: '',
        value: 0,

      },
      rules: {
        type: [
          {required: true, message: 'Please select type', trigger: 'blur'}
        ],
        comment: [
          {required: true, message: 'Please input comment', trigger: 'blur'}
        ],
        value: [
          {required: true, message: 'Please input value', trigger: 'blur'},
          {type: 'number', message: 'Value must be a number', trigger: 'blur'},
          {validator: foo, trigger: 'change'}
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit('submitForm', {...this.formData})
        }

        this.$refs.addItemForm.resetFields()
      })
    }
  }
}
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}

.type-select {
  width: 100%;
}

</style>
