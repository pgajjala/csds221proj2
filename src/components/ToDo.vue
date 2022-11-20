<template>
  <div class="container">
    <h2 class="text-center mt-5">FRAMEWORKS</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model="title" type="text" placeholder="Title" class="form-control" />
      <input v-model="description" type="text" placeholder="Description" class="form-control" />
      <input v-model="deadline" type="text" placeholder="Deadline" class="form-control" />
      <input v-model="priority" type="text" placeholder="Priority" class="form-control" />
      <button @click="submitTask" class="btn btn-warning">SUBMIT</button>
    </div>
  </div>

  <!-- Task table -->
  <table class="table table-bordered">
    <thead>
      <tr>
        <th scope="col" class="text-center">Title</th>
        <th scope="col" class="text-center">Description</th>
        <th scope="col" class="text-center">Deadline</th>
        <th scope="col" class="text-center">Priority</th>
        <th scope="col" class="text-center">Is Complete</th>
        <th scope="col" class="text-center">Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(task, index) in tasks" :key="index">
        <td>{{task.title}}</td>
        <td>{{task.description}}</td>
        <td>{{task.deadline}}</td>
        <td>{{task.priority}}</td>
        <td class="text-center">
          <input class="form-check-input" type="checkbox" checked>
        </td>
        <td>
          <div class="text-center" @click="editTask(index)">
            <button class="btn btn-primary btn-sm w-50">
              <span class="fa fa-pen-to-square"></span>
              Update
            </button>
          <div class="text-center" @click="deleteTask(index)">
            <button class="btn btn-danger btn-sm w-50">
              <span class="fa fa-circle-xmark"></span>
              Delete
            </button>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'ToDo',
  props: {
    msg: String,
  },
  data(){
    return{
      title:'',
      description:'',
      deadline:'',
      priority:'',
      is_complete:'',
      editedTask: null,
      tasks: [
      ]
    } 
  },
  
  methods: {
    submitTask(){
      if(this.title.length === 0) {
        return;
      }
      if(this.description.length === 0) {
        return;
      }
      if(this.deadline.length === 0) {
        return;
      }
      if(this.priority.length === 0) {
        return;
      }

      if(this.editedTask === null) {
        this.tasks.push({
          title: this.title,
          description: this.description,
          deadline: this.deadline,
          priority: this.priority,
          is_complete: 'true'
        });
      } else {
        this.tasks[this.editedTask].title = this.title;
        this.tasks[this.editedTask].description = this.description;
        this.tasks[this.editedTask].deadline = this.deadline;
        this.tasks[this.editedTask].priority = this.priority;
        this.editedTask = null;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.editedTask = index;
      this.title = this.tasks[index].title;
      this.description = this.tasks[index].description;
      this.deadline = this.tasks[index].deadline;
      this.priority = this.tasks[index].priority;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
