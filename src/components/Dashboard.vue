<template>
   <div class="container-fluid" style="background-color: yellowgreen">
      <div class="row">
        
        <category v-for="category in categories" 
                  :key="category.id" 
                  :dataCategory="category"
                  @getNewTask="createNewTask"
                  :categories = "categories"
                  @updatedTask="updatedTask"
                  @deleteTask="deleteTask"
                  ></category>

      </div>
    </div>
</template>

<script>
import Category from './Category.vue'

export default {
  name: "dashboard",
  props: ["categories"],
  data() {
    return {

    }
  },
  components: {
    Category

  },
  methods: {
    createNewTask(dataTask){
      return this.$emit("newTask", dataTask)
    },
    updatedTask(dataUpdatedTask){
      this.$emit("updatedTask", dataUpdatedTask)
    },
    updatedTask(dataUpdatedTask){
      this.$emit("updatedTask", dataUpdatedTask)
    },
    deleteTask(deletedTaskId){
      this.$emit("deleteTask", deletedTaskId)
    }
  }
}
</script>

<style>

</style>