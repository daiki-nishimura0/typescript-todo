<template>
  <div>
    <router-link to="/">Home</router-link>
    <v-spacer />
    <router-link to="/add">Add</router-link>
    <router-view />
  </div>
</template>

<script lang="ts">
// import axios from 'axios';
// import { Component, Vue } from 'vue-property-decorator';

// const client = axios.create({
//   baseURL: 'http://localhost:3000',
//   headers: {
//     'Contet-Type': 'application/json',
//   },
// });
// interface Task {
//   id: number;
//   done: boolean;
//   title: string;
//   description: string;
// }

// @Component
// export default class App extends Vue {
//   private task: Task[] = [];

//   private newTask = '';

//   get completedTasks(): number {
//     return this.task.filter((task) => task.done).length;
//   }
//   get progress(): number {
//     return (this.completedTasks / this.task.length) * 100;
//   }
//   get remainingTasks(): number {
//     return this.task.length - this.completedTasks;
//   }

//   public create() {
//     axios.post('http://localhost:3000/todos', {
//       done: false,
//       title: this.newTask,
//       description: '',
//     });
//     axios
//       .get('http://localhost:3000/todos')
//       .then((res) => {
//         this.task = res.data;
//       })
//       .catch(function (error) {
//         console.log(error);
//       });
//     this.newTask = '';
//   }
//   public checkDone(id: number, done: boolean) {
//     axios.patch('http://localhost:3000/todos/' + id, {
//       id: id,
//       done: done,
//     });
//     // .then(function(res){

//     // })
//   }
//   created() {
//     axios
//       .get('http://localhost:3000/todos')
//       .then((res) => {
//         this.task = res.data;
//       })
//       .catch(function (error) {
//         console.log(error);
//       });
//   }
// }
</script>
