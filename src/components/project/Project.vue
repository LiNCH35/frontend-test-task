<template>
    <project-name ref='projectNameComponent'
                  :project-name="projectName"
                  @save="projectNameSaved"
    />
    <task-tree :items="tasks"
               @update="updateTasks"
    />
</template>

<script>
    import {ref, onMounted} from 'vue';
    import ProjectName from "./ProjectName";
    import {useSessionStorage} from '../../plugins/sessionStorage';
    import TaskTree from "../task/TaskTree";

    export default {
        name: "Project",
        components: {TaskTree, ProjectName},

        setup() {
            const store = useSessionStorage();

            const projectNameComponent = ref(null);
            const projectName = ref('New Project');
            const projectNameSaved = (value) => {
                store.set('projectName', value);
            };

            const getTasks = () => {
                let items = store.get('tasks');
                return items || [];
            };
            const setTasks = value => store.set('tasks', value);
            const tasks = ref(getTasks());
            const updateTasks = (value) => {
                setTasks(value);
                tasks.value = getTasks();
            };

            onMounted(() => {
                let name = store.get('projectName');
                if (name) {
                    projectName.value = name;
                    projectNameComponent.value.setName(name);
                }

                // tasks.value = store.get('tasks');
            });

            return {
                projectNameComponent,
                projectName,
                projectNameSaved,

                tasks,
                setTasks,
                updateTasks,
            }
        }
    }
</script>

<style scoped>

</style>