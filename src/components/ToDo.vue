<template>
  <AddPopup
    v-show="isAddModalVisible"
    :existing_description="description"
    :existing_deadline="deadline"
    :existing_priority="priority"
    :tasks="tasks"
    @submitTask="submitTask"
    @close="closeAddPopup"
  />
  <EditPopup v-show="isEditModalVisible" @close="closeEditPopup" />

  <div class="container-fluid">
    <div class="card">
      <div
        class="card-header d-flex justify-content-between align-items-center"
      >
        <div class="col-sm-11">
          <h5 class="text-center">FRAMEWORKS</h5>
        </div>
        <div class="col-sm-1">
          <button
            @click="showAddModal"
            type="button"
            class="btn btn-primary btn-sm"
          >
            <span class="fa-solid fa-circle-plus"></span> Add
          </button>
        </div>
      </div>
    </div>
    <div>
      <!--Task Table-->
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
            <td>
              <span>{{ task.title }}</span>
            </td>
            <td>
              <span>{{ task.description }}</span>
            </td>
            <td>{{ task.deadline }}</td>
            <td>
              <span>{{ task.priority }}</span>
            </td>
            <td align="center">
              <label class="container">
                <input type="checkbox" v-model="tasks[index].isComplete" />
                <span class="checkmark"></span
              ></label>
            </td>
            <td>
              <div class="text-center" @click="showEditModal">
                <button class="btn btn-primary btn-sm w-50">
                  <span class="fa fa-pen-to-square"></span>
                  Update
                </button>
              </div>
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
    </div>
  </div>
</template>

<script>
import AddPopup from './AddPopup';
import EditPopup from './EditPopup';
export default {
  name: 'Todo',
  props: {
    msg: String,
  },
  components: {
    AddPopup,
    EditPopup,
  },
  data() {
    return {
      isAddModalVisible: false,
      isEditModalVisible: false,
      title: '',
      description: '',
      deadline: '',
      priority: '',
      is_complete: false,
      availablePriorities: ['Low', 'Med', 'High'],
      tasks: [],
    };
  },
  methods: {
    submitTask(title, description, deadline, priority) {
      this.tasks.push({
        title: title,
        description: description,
        deadline: deadline,
        priority: priority,
        is_complete: false,
      });
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].title;
      this.editedTask = index;
    },
    showAddModal() {
      this.isAddModalVisible = true;
    },
    closeAddPopup() {
      this.isAddModalVisible = false;
    },
    showEditModal() {
      this.isEditModalVisible = true;
    },
    closeEditPopup() {
      this.isEditModalVisible = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
