
<template>
  <div class="modal-backdrop">
    <div class="modal" id="editPopup" role="dialog">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">
              <span class="fa-solid fa-pen-to-square" ></span>
               Edit Task
            </h5>
          </div>
          <section class="modal-body">
          <form>
          <div class="form-group">
          <input type="text" class="form-control" id="title"  placeholder = "Title"> </input>
          </div>
          
          <div class = "form-group">
          <input type="text" class="form-control mt-3" id="title" placeholder = "Description"></input>
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
          <div>
            <button type="button" class="btn btn-primary" @click="close">
              <span class="fa-solid fa-circle-plus"></span> Add
            </button>
            <button type="button" class="btn btn-danger" @click="close">
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
</style>

<script>
export default {
  name: 'EditPopup',
  methods: {
    close() {
      this.$emit('close');
    },
  },
  data(){
    return {
      priority:'',
      deadline: '' 
    }
  }
};
</script>

