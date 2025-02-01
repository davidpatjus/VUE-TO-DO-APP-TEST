<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <v-card class="mx-auto pa-6 elevation-3 bg-deep-purple pb-10 px-12" max-width="1600">

          <v-card-title class="text-h5 font-weight-bold text-center mb-4">
            ✨ To Do App - David Patiño ✨
          </v-card-title>

          <!-- Formulario de Nueva Tarea -->
          <TaskForm @add-task="addTask" />

          <!-- Lista de Tareas -->
          <v-list class="mt-4 d-flex align-center rounded-lg d-flex flex-wrap">

            <!-- Mapeo de Tareas -->
            <v-list-item
              v-for="task in tasks"
              :key="task.id"
              class="rounded-lg ma-3 pa-3"
              :class="
                task.completed ? 'bg-green-accent-1' : 'bg-yellow-accent-1'
              "
            >
              <v-list-item-content>

                <!-- Titulo -->
                <v-list-item-title
                  class="text-dark font-weight-medium rounded-lg ma-3"
                >
                  {{ task.title }}
                </v-list-item-title>

                <!-- Estado de la tarea -->
                <v-chip
                  :color="task.completed ? 'success' : 'warning'"
                  small
                  outlined
                  class="mt-3 mb-1"
                >
                  {{ task.completed ? "Completado" : "Pendiente" }}
                </v-chip>

              </v-list-item-content>

              <div class="d-flex ga-3 pa-4">

                <!-- Completar -->
                <v-list-item-action>
                  <v-btn icon @click="toggleTaskCompletion(task)" color="green">
                    <v-icon>{{
                      task.completed ? "mdi-check-circle" : "mdi-circle-outline"
                    }}</v-icon>
                  </v-btn>
                </v-list-item-action>

                <!-- Editar -->
                <v-list-item-action>
                  <v-btn icon @click="editTask(task)" color="warning">
                    <v-icon>mdi-pencil</v-icon>
                  </v-btn>
                </v-list-item-action>

                <!-- Eliminar -->
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

// Obtenemos las tareas del localStorage
const tasks = ref(JSON.parse(localStorage.getItem("tasks")) || []);

// Obtenemos el siguiente id
let nextId = tasks.value.length
  ? Math.max(...tasks.value.map((t) => t.id)) + 1
  : 1;

// Guardamos las tareas en el localStorage
const saveTasks = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
};

// Añadir tarea
const addTask = (title) => {
  tasks.value.push({ id: nextId++, title, completed: false });
  saveTasks();
};

// Completar tarea
const toggleTaskCompletion = (task) => {
  task.completed = !task.completed;
  saveTasks();
};

// Editar tarea
const editTask = (task) => {
  const newTitle = prompt("Edit task:", task.title);
  if (newTitle?.trim()) {
    task.title = newTitle.trim();
    saveTasks();
  }
};

// Eliminar tarea
const deleteTask = (taskToDelete) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskToDelete.id);
  saveTasks();
};

// Observar cambios en las tareas
watch(tasks, saveTasks, { deep: true });
</script>
