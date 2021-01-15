<template>

  <div>
  <div class="col-sm my-2 mx-2 shadow rounded">
          <div class="card">
            <div class="card-body">
              <p class="card-text">
                {{ dataTask.title }}
              </p>
              <div class="col">
                <button type="button" class="btn btn-primary btn-sm shadow rounded" @click="showUpdate()"><i class="bi bi-gear"></i> Update</button>
                <button type="button" class="btn btn-primary btn-sm shadow rounded" @click="deleteTask(dataTask.id)">Delete</button>
              </div>
            </div>
          </div>
  </div>

        <!-- <task-add v-show="show" :categoryId="dataCategory.id" @newDataTask="createTask"></task-add> -->
    <!-- <task-update v-show="updateShow" :updateTask="dataTask"></task-update> -->
    <task-update v-show="updateShow" :taskId="dataTask.id" :taskTitle="dataTask.title" :taskCategoryId="dataTask.CategoryId" :categories = "categories" @updatedTask="updatedTask"></task-update>
  
  </div>
</template>

<script>
import TaskUpdate from './TaskUpdate.vue'

export default {
  components: { TaskUpdate },
  name: "Task",
  props: [
    "dataTask",
    "categories"
  ],
  data() {
    return {
      updateShow: false
    }
  },
  methods: {
    showUpdate(){
      this.updateShow= !this.updateShow
    },
    updatedTask(dataUpdatedTask){
      this.$emit("updatedTask", dataUpdatedTask)
    },
    deleteTask(idTask){
      const deletedTaskId ={
        id: idTask
      }
      this.$emit("deleteTask", deletedTaskId)
    }
  },
  // created(){
  //   console.log(this.dataTask);
  // }
}
</script>

<style>

</style>