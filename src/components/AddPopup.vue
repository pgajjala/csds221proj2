
<template>
  <div class="modal-backdrop">
    <div class="modal" id="addPopup" role="dialog">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">
              <div v-if="isAddTask" key = "addA">
                <span class="fa-solid fa-circle-plus" ></span>
                Add Task
              </div>
              <div v-else key = "updateA">
                <span class="fa-solid fa-pen-to-square" ></span>
                Edit Task
              </div>
            </h5>
          </div>
          <section class="modal-body">
          <form>
          <div class="form-group" v-if= "isAddTask">
          <label for = "title" class="ms-2 position-absolute" style="margin-top: -0.60rem"> <span class="h7 small bg-white text-muted px-1">Title</span></label>
          <input type="text" class="form-control mt-3" id="title" ref="title" v-model = "v$.title.$model" placeholder = "Title"> </input>
            <div class="input-errors" v-for="(error, index) of v$.description.$errors" :key="index">
              <div style="color:red; font-size:12px" class="error-msg">{{ error.$message }}</div>
            </div>
          </div>
          <div class = "form-group">
          <label for = "description" class="ms-2 position-absolute" style="margin-top: -0.60rem"> <span class="h7 small bg-white text-muted px-1">Description</span></label>
          <input type="text" class="form-control mt-3" id="description" placeholder = "Description" v-model= "v$.description.$model"></input>
            <div class="input-errors" v-for="(error, index) of v$.description.$errors" :key="index">
              <div style="color:red; font-size:12px" class="error-msg">{{ error.$message }}</div>
            </div>
          </div>
          <div class = "form-group">
          <label for = "deadline" class="ms-2 position-absolute" style="margin-top: -0.60rem"> <span class="h7 small bg-white text-muted px-1">Deadline</span></label>
          <input type = "date" class = "form-control mt-3" id ="deadline" v-model = "deadline">
          </div>
          <div class = "form-group">
            <div>Priority: {{priority}} </div>
            <input type="radio" name="priority" id="low" value = "Low" v-model = "priority" />
            <label for="low" class = "radio"> Low </label>
            <input type="radio" name="priority" id="med" value = "Med" v-model = "priority"/>
            <label class= "radio" for="med"> Med </label>
            <input type="radio" id="high" value = "High" v-model = "priority" name="priority"/> 

            <label for="high" class= "radio"> High </label>
            </div>
          

          </section>

          <footer class="modal-footer">
            <div v-if = "isAddTask" key = "addButton">
              <button type="button" class="btn btn-block btn-primary" @click="submitTask">
               Add
              </button>
              <button type="button" class="btn btn-block btn-danger" @click="close">
              <span class="fa-solid fa-circle-xmark"></span> Cancel
              </button>
            </div>
            <div v-else key = "updateButton">
              <button type="button" class="btn btn-block btn-primary" @click="editTask">
              <span class="fa-solid fa-pen-to-square"></span> Edit
              </button>
              <button type="button" class="btn btn-block btn-danger" @click="close">
              <span class="fa-solid fa-circle-xmark"></span> Cancel
              </button>
            </div>
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4;
  margin: 1;
}

.modal {
  background: rgba(240, 248, 255, 0.18);
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  background: blue;
  color: white;
  justify-content: center;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
  margin: 5;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}

.has-error {
    border: 1px solid red;
}
</style>

<script>
import useVuelidate from '@vuelidate/core';
import { required } from '@vuelidate/validators';

export default {
  name: 'AddPopup',
  props: {
    isModalVisible: Boolean,
    isAddTask: Boolean,
    existing_description: String,
    existing_deadline: String,
    existing_priority: String,
    tasks: Array
  },
  methods: {
    submitTask(title, description, deadline, priority){
      this.v$.$validate()
      if(!this.v$.$error) {
        const[year, month, day] = this.deadline.split('-');
        this.$emit('submitTask',this.title, this.description, `${month}/${day}/${year}`, this.priority);
        this.clear();
        this.close(); 
      } 
    },
    close() {
      this.$emit('close');
    },
    clear(){
      this.title = '';
      this.description = '';
      this.deadline = '';
      this.priority = 'low';
    },
    editTask(){
      const[year, month, day] = this.deadline.split('-');
      this.$emit('editTask', this.description, `${month}/${day}/${year}`, this.priority);
      this.clear();
      this.close();
    }
  },
  setup () {
    return { v$: useVuelidate() }
  },
  data() {
    return {
      title: '',
      description: '',
      priority:'',
      deadline: '',
      priority:'',
      date: '',
    }
  },
  validations() {
    return {
      title: {
        required, title_validation: {
            $message: 'Invalid Name. Valid name only contain letters, dashes (-) and spaces'
          } 
      },
      description: {
        required, description_validation: {
            $message: 'Invalid Name. Valid name only contain letters, dashes (-) and spaces'
          } 
      }
    }
  }
};
</script>

