<template>
  <div class="card w-50 p-4 mt-4 mx-auto">
    <form class="input-group mb-3" @submit.prevent="addTask">
        <input type="text" class="form-control" placeholder="Type Your Task and Press Enter.." v-model="newTask">
        <!-- <button class="btn btn-success" type="button">Add Task</button> -->
    </form>
    <div class="d-flex justify-content-start align-items-center mb-3">
      <a href="javascript:" class="text-decoration-none text-muted" @click="filterTodos = 'all'">All ({{ todoItems }})</a>
      <a href="javascript:" class="text-decoration-none text-muted mx-4" @click="filterTodos = 'pending'">Pending ({{ pendingTask }})</a>
      <a href="javascript:" class="text-decoration-none text-muted" @click="filterTodos = 'done'">Done ({{ doneTask }})</a>
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item d-flex justify-content-between align-items-center" :class="{task_done : todo.status}" v-for="(todo, index) in filterTask" :key="todo.id" @click="taskDone(todo)">
        <span class="">
          {{todo.task}}
          <small class="text-muted fw-light d-block">{{ todo.time }}</small>
        </span>
        <a href="javascript:" class="text-decoration-none text-danger" @click="removeTask(index)">&#9932;</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todoapp',
  data() {
    return {
      newTask: '',
      todos: [
        {
          id: 1,
          task : 'This is Task one',
          status: false,
          time : '2 mins ago'
        },
        {
          id: 2,
          task : 'This is Task Two',
          status: false,
          time : '1 hour ago'
        },
        {
          id: 3,
          task : 'This is Task Three',
          status: false,
          time : '5 hours ago'
        },
        {
          id: 4,
          task : 'This is Task Four',
          status: true,
          time : '1 day ago'
        },
      ],
      filterTodos: 'all'
    };
  },
  methods: {
    
    addTask() {
      let today = new Date();
      let houre = today.getHours();
      let minute = today.getMinutes();
      let thisTime = `${houre}: ${minute}`;
      var date = today.getDate() + '-' + (today.getMonth() + 1) + '-' + today.getFullYear();
      const todo ={
        id: this.newTask,
        task: this.newTask,
        status: false,
        time: 'Task Added: ' + date + ' at: ' + thisTime
      }
      this.todos.unshift(todo);
      this.newTask = ''
    },
    taskDone(todo){
      todo.status = !todo.status;
    },
    removeTask(index){
      this.todos.splice(index, 1);
    }
  },
  computed: {
    filterTask(){
      if (this.filterTodos == 'all') return this.todos;
      if (this.filterTodos == 'done') return this.todos.filter((todo) => todo.status);
      if (this.filterTodos == 'pending') return this.todos.filter((todo) => !todo.status);
    },
    todoItems(){
      return this.todos.length;
    },
    doneTask(){
      return this.todos.filter(todo => todo.status).length;
    },
    pendingTask(){
      return this.todos.filter(todo => !todo.status).length;
    }
  }
}
</script>

<style scoped>
  .form-control{
    height: 50px;
  }
  .form-control:focus{
    box-shadow: none!important;
  }
  .list-group{
    max-height: 300px;
    overflow-y: auto;
    cursor: pointer;
  }
  .list-group-item{
    transition: .4s all;
  }
  .task_done{
    cursor:default;
    color: seagreen;
    border-left: 4px solid seagreen!important;
    background-color: rgba(106, 255, 170, 0.219) ;
  }
  .list-group::-webkit-scrollbar {
    width: 3px;
  }
  
  .list-group::-webkit-scrollbar-track {
    box-shadow: inset 0 0 6px rgb(208, 252, 235);
  }
  
 .list-group::-webkit-scrollbar-thumb {
    background-color: rgb(185, 185, 185);
    outline: 1px solid rgb(185, 185, 185);
  }
</style>