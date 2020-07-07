<template>
    <div v-for="(task, key) in items" :key="`${level}-${key}`">
        <form @submit="save" @reset="reset" v-if="editMode === key">
            <input v-model="task.title">
            <h3>{{ task.status }}</h3>
            <span>{{ task.description }}</span>
<!--            <task-tree v-for="childTask in task.children"-->
<!--                       :title="childTask.title"-->
<!--                       :status="childTask.status"-->
<!--                       :description="childTask.description"-->
<!--            />-->
            <button type="submit">Save</button>
        </form>

        <div v-else>
            <h3>{{ task.title }}</h3>
            <h3>{{ task.status }}</h3>
            <span>{{ task.description }}</span>
            <task-tree :items="task.children"
                       @update="updateByKey($event, key)"
                       :level="level + 1"
            />
            <button @click="editMode = key">Edit</button>
        </div>
    </div>
    <button @click="add">Add</button>
</template>

<script>
    import {ref, nextTick} from 'vue';

    /**
     * @Component TaskTree
     * Recursive
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
        setup(props, context) {
            const editMode = ref(-1);

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

            const updateByKey = (value, key) => {
                console.log(value);
                console.log(key);
                console.log(props.items);
                if (props.items[key]) {
                    let items = Object.assign([], props.items)
                    items[key].children = value;
                    console.log(items);
                    context.emit('update', items);
                }
                console.log(props.items);
            };

            return {
                editMode,
                save,
                reset,
                add,
                updateByKey
            }
        }
    }
</script>

<style scoped>

</style>