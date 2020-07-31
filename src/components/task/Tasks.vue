<template>
  <task-tree
      v-model:items="tasks"
  />
</template>

<script>
import TaskTree from "./TaskTree";
import {ref, computed} from "vue";
import {useSessionStorage} from "@/plugins/sessionStorage";
import {compareObjects} from '@/plugins/objectHelper'

/**
 * @Component Tasks
 * Root of Task tree
 */
export default {
  name: "Tasks",
  components: {TaskTree},

  setup() {
    const store = useSessionStorage()

    const getTasksFromStore = () => {
      let items = store.get('tasks')
      return items || []
    }
    const setTasksToStore = value => store.set('tasks', value)

    const getTrigger = ref(0)
    const tasks = computed({
      get: () => {
        getTrigger.value = +getTrigger.value;
        return getTasksFromStore();
      },
      set: value => {
        if (!compareObjects(value, getTasksFromStore())) {
          setTasksToStore(value);
          getTrigger.value++;
        }
      }
    })

    return {
      tasks,
    }
  }
}
</script>

<style scoped>

</style>