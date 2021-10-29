<template>
  <v-container style="max-width: 800px">
    <v-app-bar dark color="blue">
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Todo</v-toolbar-title>
    </v-app-bar>

    <h2 class="text-h4 success--text pl-4">
      Tasks:
      <v-fade-transition leave-absolute>
        <span :key="`task-${task.length}`">
          {{ task.length }}
        </span>
      </v-fade-transition>
    </h2>

    <v-divider class="mt-4"></v-divider>

    <strong class="mx-4 info--text text--darken-2"> 未完了: {{ remainingTasks }} </strong>

    <strong class="mx-4 success--text text--darken-2"> 完了: {{ completedTasks }} </strong>

    <v-spacer></v-spacer>

    <v-progress-circular :value="progress"></v-progress-circular>

    <v-divider class="mb-4"></v-divider>

    <v-card v-if="task.length > 0">
      <v-slide-y-transition class="py-0" group>
        <template v-for="(task, i) in task">
          <v-divider v-if="i !== 0" :key="`${i}-divider`"></v-divider>

          <v-list-item :key="`${i}-${task}`">
            <v-list-item-action>
              <v-checkbox v-model="task.done" @click="checkDone(task.id, task.done)" :color="(task.done && 'grey') || 'primary'">
                <template v-slot:label>
                  <div :class="(task.done && 'grey--text') || 'primary--text'" class="ml-4" v-text="task.title"></div>
                </template>
              </v-checkbox>
            </v-list-item-action>

            <v-spacer></v-spacer>

            <v-scroll-x-transition>
              <v-icon v-if="task.done" color="success"> mdi-check </v-icon>
            </v-scroll-x-transition>
          </v-list-item>
        </template>
      </v-slide-y-transition>
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
export default class App extends Vue {
  private task: Task[] = [];

  private newTask = '';

  get completedTasks(): number {
    return this.task.filter((task) => task.done).length;
  }
  get progress(): number {
    return (this.completedTasks / this.task.length) * 100;
  }
  get remainingTasks(): number {
    return this.task.length - this.completedTasks;
  }

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
  public checkDone(id: number, done: boolean) {
    axios.patch('http://localhost:3000/todos/' + id, {
      id: id,
      done: done,
    });
    // .then(function(res){

    // })
  }
  created() {
    axios
      .get('http://localhost:3000/todos')
      .then((res) => {
        this.task = res.data;
      })
      .catch(function (error) {
        console.log(error);
      });
  }
}
</script>
