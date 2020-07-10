<template>
    <div v-for="(task, key) in items"
         :key="`${level}-${key}`"
         :class="level === 0 ? 'main-task' : 'main-task'"
         class="task"
    >
        <form @submit="save" @reset="reset" v-if="editMode === key">
            <label>
                <input type="checkbox" v-model="task.status">
            </label>
            <label>
                <input v-model="task.title">
            </label>
            <span>{{ task.description }}</span>
            <!--            <task-tree v-for="childTask in task.children"-->
            <!--                       :title="childTask.title"-->
            <!--                       :status="childTask.status"-->
            <!--                       :description="childTask.description"-->
            <!--            />-->
            <button type="submit">Save</button>
        </form>

        <div v-else>
            <label>
                <input type="checkbox" disabled v-model="task.status">
            </label>
            <span class="title">{{ task.title }}</span>
            <button @click="editMode = key" class="button edit-button">
                Edit
            </button>
            <button @click="remove(key)" class="button remove-button">
                Remove
            </button>
            <span>{{ task.description }}</span>
            <p @click="openSubTasks(key)"
               class="sub-tasks-button"
            >
                subtasks ({{task.children.length}})
            </p>
            <div v-if="visibleSubTasks.includes(key)" class="child-tasks">
                <task-tree :items="task.children"
                           @update="updateByKey($event, key)"
                           :level="level + 1"
                />
            </div>
        </div>
    </div>
    <button @click="add">Add</button>
</template>

<script>
    import {ref, nextTick} from 'vue';

    /**
     * @Component TaskTree
     * Tasks tree. Recursive
     * @props items : Tasks[],
     * @props level : int, currentLevel
     * @emit 'update(Tasks[])' : $event - updated array of tasks
     */
    export default {
        name: "TaskTree",

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
            items: Array,
            level: {
                default: 0,
            },
        },
        emits: [
            'update',
        ],
        setup(props, context) {
            const editMode = ref(-1);

            const visibleSubTasks = ref([]);
            const openSubTasks = (index) => {
                let findIndex = visibleSubTasks.value.indexOf(index);
                if (findIndex === -1) {
                    visibleSubTasks.value.push(index);
                } else {
                    visibleSubTasks.value.splice(findIndex, 1);
                }
            }

            const save = () => {
                context.emit('update', props.items);
                editMode.value = -1;
            };
            const reset = () => {
                editMode.value = -1;
            };
            const add = () => {
                let newItem = {
                    title: 'New Task',
                    status: false,
                    description: '',
                    children: [],
                };
                let items = Object.assign([], props.items)
                items.push(newItem);
                context.emit('update', items);
                nextTick(() => {
                    editMode.value = props.items.length;
                });
            };
            const remove = (index) => {
                if (props.items[index]) {
                    let items = Object.assign([], props.items);
                    items.splice(index, 1);
                    context.emit('update', items);
                } else {
                    throw new Error("Task not found!");
                }
            };

            const updateByKey = (value, key) => {
                if (props.items[key]) {
                    let items = Object.assign([], props.items)
                    items[key].children = value;
                    context.emit('update', items);
                }
            };

            return {
                editMode,
                visibleSubTasks,
                openSubTasks,
                save,
                reset,
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
        cursor: pointer ;
        /*border-bottom: solid 1px;*/
    }

    .button {
        border: solid 1px;
        border-radius: 4px;
        padding: 4px 8px 4px 8px;
        margin-left: 12px;
    }
    .edit-button {
        background-color: yellow;
        border-color: yellow;
    }
    .edit-button:hover {
        background-color: #d2d22b;
        border-color: #d2d22b;
    }
    .remove-button {
        background-color: red;
        border-color: red;
    }
    .remove-button:hover {
        background-color: #db2b2b;
        border-color: #db2b2b;
    }
</style>