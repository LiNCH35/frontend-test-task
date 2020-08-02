<template>
  <div class="project-name">
        <span v-if="!editMode"
              @click="switchToInput"
        >
            {{ name }}
        </span>
    <div v-else>
      <label>
        <input v-model="name"
               ref="nameInput"
               @blur="save"
               @keyup.enter="save"
        >
      </label>
    </div>
  </div>
</template>

<script>
import {ref, nextTick, watch} from 'vue';

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
      name.value = value
    }
    const getName = () => (name.value ? name.value.toString() + ' | ' : '') + 'Todo-test'
    const setTitle = () => {
      if (document && props.projectName) {
        document.title = getName()
      }
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
      editMode.value = false
      context.emit('save', name.value)
      setTitle()
    }


    watch(
        () => (props.projectName),
        () => {
          setTitle()
        }
    )

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
.project-name {
  margin-left: 20px;
  color: dimgray;
  font-size: 32px;
}

.project-name input {
  color: dimgray;
  font-size: 32px;
  padding: 0;
  border: 0;
}
</style>
