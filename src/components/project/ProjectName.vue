<template>
    <h1 v-if="!editMode"
        @click="switchToInput"
    >
        {{ name }}
    </h1>
    <div v-else>
        <label>
            <input v-model="name"
                   ref="nameInput"
                   @blur="save"
                   @keyup.enter="save"
            >
        </label>
    </div>
</template>

<script>
    import {ref, nextTick} from 'vue';

    export default {
        name: "ProjectName",

        props: {
            projectName: {
                default: 'New Project',
            }
        },
        setup(props, context) {
            const name = ref(props.projectName);
            const editMode = ref(false);
            const nameInput = ref(null);

            const setName = (value) => {
                name.value = value;
            }
            const switchToInput = () => {
                editMode.value = true;
                nextTick(() => {
                    if (nameInput.value) {
                        nameInput.value.select();
                    }
                });
            }
            const save = () => {
                editMode.value = false;
                context.emit('save', name.value);
            }

            return {
                name,
                setName,
                editMode,
                nameInput,
                switchToInput,
                save,
            }
        }
    }
</script>

<style scoped>

</style>