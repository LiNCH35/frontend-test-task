<template>
  <div
      v-for="(task, key) in items"
      :key="`${level}-${key}`"
      class="task main-task"
  >
    <task-editor
        v-if="editMode === key"
        :task="task"
        @save="save"
        @reset="editMode = null"
    />

    <div v-else>
      <input type="checkbox" disabled v-model="task.status">
      <span class="title">{{ task.title }}</span>
      <button @click="editMode = key" class="button edit-button">
        Edit
      </button>
      <button @click="remove(key)" class="button remove-button">
        Remove
      </button>

      <span>{{ task.description }}</span>
      <p
          @click="toggleSubTasks(key)"
          class="sub-tasks-button"
      >
        subtasks ({{ task.children.length }})
      </p>
      <div v-if="visibleSubTasks.has(key)" class="child-tasks">
        <task-tree
            :items="task.children"
            :level="level + 1"
            @update:items="updateByKey($event, key)"
        />
      </div>
    </div>
  </div>

  <button @click="add">Add</button>
</template>

<script>
import {ref, nextTick} from 'vue'
import TaskEditor from "@/components/task/TaskEditor"

/**
 * @Component TaskTree
 * Tasks tree. Recursive
 * @props items : Tasks[],
 * @props level : int, currentLevel
 * @emit 'update:items(Tasks[])' : $event - updated array of tasks
 */
export default {
  name: "TaskTree",
  components: {TaskEditor},
  props: {
    /**
     * array of Tasks
     * Task {
     *     title - Task name,
     *     status - Task status. If the task is done - true,
     *     description - Description,
     *     children - Child tasks,
     * }
     */
    items: {
      type: Array,
      required: true,
    },
    level: {
      default: 0,
    },
  },
  emits: ['update:items'],

  setup(props, context) {
    const editMode = ref(null)

    const visibleSubTasks = ref(new Set())
    const toggleSubTasks = (index) => visibleSubTasks.value.has(index)
        ? visibleSubTasks.value.delete(index)
        : visibleSubTasks.value.add(index)

    const save = () => {
      context.emit('update:items', props.items)
      editMode.value = null
    }
    const add = () => {
      context.emit('update:items', [...props.items, {
        title: 'New Task',
        status: false,
        description: '',
        children: [],
      }])

      nextTick(() => editMode.value = props.items.length - 1)
    }
    const remove = (index) => {
      if (!props.items[index]) {
        throw new Error("Task not found!")
      }

      context.emit('update:items', props.items.filter((item, id) => id !== index))
    }

    const updateByKey = (value, key) => {
      if (props.items[key]) {
        let items = [...props.items]
        items[key].children = value
        context.emit('update:items', items)
      }
    }

    return {
      editMode,
      visibleSubTasks,
      toggleSubTasks,
      save,
      add,
      remove,
      updateByKey,
    }
  }
}
</script>

<style scoped>
.main-task {
  border: solid 1px darkgray;
  margin-bottom: 12px;
  padding: 8px;
}

.sub-task {
  border-bottom: solid 1px darkgray;
  margin-left: 12px;
}

.sub-tasks-button {
  cursor: pointer;
  /*border-bottom: solid 1px;*/
}

.button {
  border: solid 1px;
  border-radius: 4px;
  padding: 4px 8px 4px 8px;
  margin-left: 12px;
}

.edit-button {
  background-color: #9ccc65;
  border-color: #9ccc65;
}

.edit-button:hover {
  background-color: #8bc34a;
  border-color: #8bc34a;
}

.remove-button {
  background-color: #ec407a;
  border-color: #ec407a;
}

.remove-button:hover {
  background-color: #e91e63;
  border-color: #e91e63;
}
</style>