<template>
  <v-form @submit.prevent="submitTask" class="d-flex align-center ga-2">
    <v-text-field
      v-model="taskTitle"
      label="Nueva tarea"
      class="flex-grow-1 mr-2"
      variant="solo"
      color="deep-purple-accent-2"
      dense
      rounded
      :rules="[(v) => !!v || 'El título es obligatorio']"
      required
    ></v-text-field>
    <v-btn
      type="submit"
      color="deep-purple-accent-2"
      class="mb-6"
      :disabled="!taskTitle.trim()"
    >
      <v-icon>mdi-plus</v-icon>
    </v-btn>
  </v-form>
</template>

<script>
import { ref } from "vue";

export default {
  emits: ["add-task"],
  setup(_, { emit }) {
    const taskTitle = ref("");

    // Emitir el evento "add-task" con el título de la tarea
    const submitTask = () => {
      if (taskTitle.value.trim()) {
        emit("add-task", taskTitle.value.trim());
        taskTitle.value = "";
      }
    };

    return { taskTitle, submitTask };
  },
};
</script>
