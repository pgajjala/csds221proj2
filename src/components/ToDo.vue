<template>
  <AddPopup
    v-show="isModalVisible"
    :isModalVisible="isModalVisible"
    :isAddTask="isAddTask"
    :existing_description="description"
    :existing_deadline="deadline"
    :existing_priority="priority"
    :tasks="tasks"
    @submitTask="submitTask"
    @editTask="editTask"
    @close="closePopup"
  />
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
            @click="submitTaskPopup"
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
              <input
                type="checkbox"
                v-model="tasks[index].isComplete"
                @click="tasks[index].isComplete = !tasks[index].isComplete"
              />
            </td>
            <td>
              <div
                v-if="!tasks[index].isComplete"
                class="text-center"
                @click="editTaskPopup(index)"
              >
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
export default {
  name: 'Todo',
  props: {
    msg: String,
  },
  components: {
    AddPopup,
  },
  data() {
    return {
      isModalVisible: false,
      isAddTask: true,
      title: '',
      description: '',
      deadline: '',
      priority: '',
      availablePriorities: ['Low', 'Med', 'High'],
      tasks: [],
    };
  },
  methods: {
    submitTaskPopup() {
      this.isAddTask = true;
      this.showPopup();
    },
    editTaskPopup(index) {
      this.taskIndex = index;
      this.isAddTask = false;
      this.description = this.tasks[this.taskIndex].description;
      this.deadline = this.tasks[this.taskIndex].deadline;
      this.priority = this.tasks[this.taskIndex].priority;
      this.showPopup();
    },
    submitTask(title, description, deadline, priority) {
      this.tasks.push({
        title: title,
        description: description,
        deadline: deadline,
        priority: priority,
        is_complete: false,
      });
      this.$toast.success('Task successfully added');
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.$toast.error('Task successfully deleted');
    },
    editTask(index) {
      this.tasks[this.taskIndex].description = description;
      this.tasks[this.taskIndex].deadline = deadline;
      this.tasks[this.taskIndex].priority = priority;
      this.$toast.warning('Task successfully edited');
    },
    showPopup() {
      this.isModalVisible = true;
    },
    closePopup() {
      this.isModalVisible = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
