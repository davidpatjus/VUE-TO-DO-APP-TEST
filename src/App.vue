<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <v-card class="mx-auto pa-6 elevation-3" max-width="480">
          <v-card-title class="text-h5 font-weight-bold text-center mb-4">
            ✨ To Do App - David Patiño ✨
          </v-card-title>

          <!-- Formulario de Nueva Tarea -->
          <TaskForm @add-task="addTask" />

          <!-- Lista de Tareas -->
          <v-list class="mt-4 d-flex align-center">
            <v-list-item
              v-for="task in tasks"
              :key="task.id"
              class="rounded-lg mb-3 pa-3 bg-grey-lighten-1"
              :class="
                task.completed ? 'bg-success-lighten-3' : 'bg-info-lighten-3'
              "
            >
              <v-list-item-content>
                <v-list-item-title
                  class="text-dark font-weight-medium rounded-lg pa-2 mb-2"
                >
                  {{ task.title }}
                </v-list-item-title>
                <v-chip
                  :color="task.completed ? 'success' : 'warning'"
                  small
                  outlined
                  class="mt-1"
                >
                  {{ task.completed ? "Completado" : "Pendiente" }}
                </v-chip>
              </v-list-item-content>

              <div class="d-flex ga-3 pa-2">
                <v-list-item-action>
                  <v-btn icon @click="toggleTaskCompletion(task)" color="green">
                    <v-icon>{{
                      task.completed ? "mdi-check-circle" : "mdi-circle-outline"
                    }}</v-icon>
                  </v-btn>
                </v-list-item-action>

                <v-list-item-action>
                  <v-btn icon @click="editTask(task)" color="warning">
                    <v-icon>mdi-pencil</v-icon>
                  </v-btn>
                </v-list-item-action>

                <v-list-item-action>
                  <v-btn icon @click="deleteTask(task)" color="error">
                    <v-icon>mdi-delete</v-icon>
                  </v-btn>
                </v-list-item-action>
              </div>
            </v-list-item>
          </v-list>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, watch } from "vue";
import TaskForm from "./components/TaskForm.vue";

const tasks = ref(JSON.parse(localStorage.getItem("tasks")) || []);

let nextId = tasks.value.length
  ? Math.max(...tasks.value.map((t) => t.id)) + 1
  : 1;

const saveTasks = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
};

const addTask = (title) => {
  tasks.value.push({ id: nextId++, title, completed: false });
  saveTasks();
};

const toggleTaskCompletion = (task) => {
  task.completed = !task.completed;
  saveTasks();
};

const editTask = (task) => {
  const newTitle = prompt("Edit task:", task.title);
  if (newTitle?.trim()) {
    task.title = newTitle.trim();
    saveTasks();
  }
};

const deleteTask = (taskToDelete) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskToDelete.id);
  saveTasks();
};

watch(tasks, saveTasks, { deep: true });
</script>
