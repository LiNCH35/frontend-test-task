<template>
    <project-name @save="projectNameSaved"
    />
</template>

<script>
    import {} from 'vue';
    import ProjectName from "./ProjectName";

    export default {
        name: "Project",
        components: {ProjectName},

        setup() {
            const projectNameSaved = (value) => {
                console.log('saved');
                console.log(value);
            };

            return {
                projectNameSaved,
            }
        }
    }
</script>

<style scoped>

</style>