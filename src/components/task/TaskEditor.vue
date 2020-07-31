<template>
  <form
      @submit="save"
      @reset="reset"
  >
    <input type="checkbox" v-model="editableTask.status">
    <input v-model="editableTask.title">
    <span>{{ task.description }}</span>
    <button type="submit">Save</button>
    <button type="reset">Reset</button>
  </form>
</template>

<script>
import { toRefs } from 'vue'

export default {
  name: "TaskEditor",
  emits: ['save', 'reset'],

  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  setup(props, {emit}) {
    const {task: editableTask} = toRefs(props)

    const reset = () => {
      editableTask.value = props.task;
      emit('reset')
    }

    const save = () => {
      emit('save', editableTask)
    }

    return {
      editableTask,
      save,
      reset,
    }
  },
}
</script>

<style scoped>

</style>