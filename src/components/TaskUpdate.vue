<template>
    <div class="col-sm my-2 mx-2 shadow rounded" v-show="closeShow">
          <div class="card">
            <div class="card-body">
            <form @submit.prevent="updateTask(taskId)">
              <textarea id="textUpdate" class="form-control" rows="3" v-model="title"></textarea>


                <select class="form-select" name="template" v-model="selected">
                    <option v-for="item in categories" :key="item.id" v-bind:value="item.id">
                      {{ item.name }}
                    </option>
                </select>

              <div class="col">
                <button type="submit" class="btn btn-primary btn-sm shadow rounded">Yes</button>
                <button type="button" class="btn btn-primary btn-sm shadow rounded" @click="showUpdate()">Cancel</button>
              </div>
            </form>
            </div>
          </div>
  </div>
</template>

<script>
export default {
  name: "TaskUpdate",
  props: ["taskId", "taskTitle", "categories", "taskCategoryId"],
  data(){
    return{
      closeShow: true,
      title: this.taskTitle,
      selected: this.taskCategoryId
    }
  },
  methods:{
    updateTask(taskId){
      const dataUpdatedTask = {
        id: taskId,
        title: this.title,
        CategoryId: this.selected
      }
      this.$emit("updatedTask", dataUpdatedTask)
      this.showUpdate()
    },
    showUpdate(){
      this.closeShow = !this.closeShow
    },
  },

  // created(){
  //   console.log(this.taskId);
  // }
}
</script>

<style>

</style>