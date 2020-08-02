<template>
  <form
      @submit.prevent="save"
      @reset.prevent="reset"
      class="task-edit-form"
  >
    <div>
      <input type="checkbox" v-model="editableTask.status">
      <input v-model="editableTask.title">
      <button type="submit">Save</button>
      <button type="reset">Reset</button>
    </div>
    <div class="w-100">
      <textarea v-model="editableTask.description"></textarea>
    </div>
  </form>
</template>

<script>
import {toRefs, readonly, onBeforeUnmount} from 'vue'

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
    const {
      title: titleInitial,
      status: statusInitial,
      description: descriptionInitial
      /*, children*/
    } = readonly(props.task)

    const reset = () => {
      editableTask.value.title = titleInitial
      editableTask.value.status = statusInitial
      editableTask.value.description = descriptionInitial
      emit('reset')
    }

    const save = () => {
      emit('save', editableTask)
    }

    onBeforeUnmount(() => {
      reset()
    })

    return {
      editableTask,
      save,
      reset,
    }
  },
}
</script>

<style scoped>
.task-edit-form {
  display: flex;
  align-items: center;
}

.task-edit-form textarea {
  width: 60%;
}

.task-edit-form .w-100 {
  width: 100%;
}

/*.task-edit-form div {*/
/*  margin: auto 0;*/
/*  width: 33.333%;*/
/*}*/
</style>