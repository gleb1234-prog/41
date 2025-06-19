<template>
  <v-app>
    <v-main>
      <v-container class="mt-5">
        <v-card max-width="600" class="mx-auto">
          <v-card-title class="bg-primary">
            <span class="text-h5 text-white">To-Do List</span>
          </v-card-title>

          <v-card-text>
            <!-- Добавление новой задачи -->
            <v-text-field
              v-model="newTask"
              label="Новая задача"
              @keyup.enter="addTask"
              clearable
            >
              <template v-slot:append>
                <v-btn @click="addTask" color="primary" icon="mdi-plus"></v-btn>
              </template>
            </v-text-field>

            <!-- Список задач -->
            <v-list>
              <v-list-item
                v-for="(task, index) in tasks"
                :key="index"
                :class="{ 'text-decoration-line-through': task.done }"
              >
                <template v-slot:prepend>
                  <v-checkbox v-model="task.done"></v-checkbox>
                </template>

                <v-list-item-title>{{ task.text }}</v-list-item-title>

                <template v-slot:append>
                  <v-btn
                    @click="deleteTask(index)"
                    icon="mdi-delete"
                    color="error"
                    variant="text"
                  ></v-btn>
                </template>
              </v-list-item>
            </v-list>
          </v-card-text>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([
  { text: 'Изучить Vuetify', done: false },
  { text: 'Создать To-Do List', done: true }
])

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, done: false })
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}
</script>