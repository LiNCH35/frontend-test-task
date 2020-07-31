<template>
    <project-name ref='projectNameComponent'
                  :project-name="projectName"
                  @save="projectNameSaved"
    />
    <hr>
    <tasks />
</template>

<script>
    import {ref, onMounted} from 'vue';
    import ProjectName from "./ProjectName";
    import {useSessionStorage} from '@/plugins/sessionStorage';
    import Tasks from "../task/Tasks";

    export default {
        name: "Project",
        components: {Tasks, ProjectName},

        setup() {
            const store = useSessionStorage();

            const projectNameComponent = ref(null);
            const projectName = ref('New Project');
            const projectNameSaved = (value) => {
                store.set('projectName', value);
            };

            onMounted(() => {
                let name = store.get('projectName');
                if (name) {
                    projectName.value = name;
                    projectNameComponent.value.setName(name);
                }
            });

            return {
                projectNameComponent,
                projectName,
                projectNameSaved,
            }
        }
    }
</script>

<style scoped>

</style>