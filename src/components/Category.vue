<template>
  <div class="card col-sm mx-2 p-0">
  <div class="card-header">{{ dataCategory.name }}</div>
    <div class="card-body p-2">
      <div class="overflow-auto" style="max-height: 73vh;">

        <task v-for="task in dataCategory.Tasks" :key="task.id" :dataTask="task"></task>

        <task-add v-show="show"></task-add>
      </div>
    </div>
  <div class="card-footer d-grid gap-2">
  <button class="btn btn-primary" type="button" 
          @click="showAddForm();"
          >Button</button>
  </div>
  </div>
</template>

<script>
import Task from './Task.vue';
import TaskAdd from './TaskAdd.vue';

export default {
  name: "category",
  props: ["dataCategory"],
  data() {
    return {
      show: false,
      title: ""
    } 
  },
  components: {
    Task,
    TaskAdd  
  },
  methods: {
    focusEditor(){
      this.$refs.editor.focus()
      // console.log(this.$refs)
    },
    createNewTask(id){
      const dataTask = { CategoryId: id, title:this.title }
      // console.log(dataTask);
      this.$emit("newDataTask", dataTask)
      this.removeAddForm()
    },
    showAddForm(){
      // this.focusEditor()
      this.show = true
      this.title = ""
    },
    removeAddForm(){
      this.show = false
      this.title = ""
    }
  },
}
</script>

<style>

</style>