<template>
  <v-container style="max-width: 800px">
    <v-card class="mx-a" outlined>
      <v-app-bar dark color="blue">
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
        <v-toolbar-title>Todo</v-toolbar-title>
      </v-app-bar>

      <v-card class="mx-a" outlined>
        <v-text-field v-model="newTask" label="Todoを入力してね" @keydown.enter="create" filled outlined single-line>
          <template v-slot:append>
            <v-fade-transition>
              <v-icon v-if="newTask" @click="create"> mdi-pencil </v-icon>
            </v-fade-transition>
          </template>
        </v-text-field>
      </v-card>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import axios from 'axios';
import { Component, Vue } from 'vue-property-decorator';

const client = axios.create({
  baseURL: 'http://localhost:3000',
  headers: {
    'Contet-Type': 'application/json',
  },
});
interface Task {
  id: number;
  done: boolean;
  title: string;
  description: string;
}

@Component
export default class AddTask extends Vue {
  private task: Task[] = [];

  private newTask = '';

  public create() {
    axios.post('http://localhost:3000/todos', {
      done: false,
      title: this.newTask,
      description: '',
    });
    axios
      .get('http://localhost:3000/todos')
      .then((res) => {
        this.task = res.data;
      })
      .catch(function (error) {
        console.log(error);
      });
    this.newTask = '';
  }
}
</script>
