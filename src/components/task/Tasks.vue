<template>
    <task-tree :items="tasks"
               @update="updateTasks"
    />
</template>

<script>
    import TaskTree from "./TaskTree";
    import {ref} from "vue";

    /**
     * @Component Tasks
     * Root of Task tree
     * @props getTasks : function, getter
     * @props setTasks : function, setter
     */
    export default {
        name: "Tasks",
        components: {TaskTree},

        props: {
            getTasks: () => {},
            setTasks: () => {},
        },
        setup(props) {
            const tasks = ref(props.getTasks());
            const updateTasks = (value) => {
                props.setTasks(value);
                tasks.value = props.getTasks();
            };

            return {
                updateTasks,
                tasks,
            }
        }
    }
</script>

<style scoped>

</style>