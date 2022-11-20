<template>
  <div class="container">
    <h2 class="text-center mt-5">FRAMEWORKS</h2>

    <!-- Input -->
    <div class="d-flex">
      <input type="text" placeholder="Enter task" class="form-control" />
      <button class="btn btn-warning rounded-0">SUBMIT</button>
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
      <td>Title</td>
      <td>Description</td>
      <td>Deadline</td>
      <td>Priority</td>
      <td>True or False</td>
      <td>
        <div class="text-center">
          <button class="btn btn-primary btn-sm w-50">
            <span class="fa fa-pen-to-square"></span>
            Update
          </button>
        <div class="text-center">
          <button class="btn btn-danger btn-sm w-50">
            <span class="fa fa-circle-xmark"></span>
            Delete
          </button>
        </div>
      </td>
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
      tasks: [
        {
          title: 'Title',
          description: 'Description',
          deadline: 'Deadline',
          priority: 'Priority',
          is_complete: 'True or False'
        }
      ]
    } 
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
