<template>
        <div class="col-sm my-2 mx-2 shadow rounded" v-show="show">
          <div class="card">
            <div class="card-body">
            <form @submit.prevent="createNewTask(categoryId)">
              <textarea class="form-control" v-model="title" ref="editor" rows="3"></textarea>

              <div class="col mt-2">
                <button type="submit" class="btn btn-primary btn-sm shadow rounded">Create</button>
                <button type="button" class="btn btn-primary btn-sm shadow rounded" 
                @click="removeAddForm()">Cancel</button>
              </div>
            </form>
            </div>
          </div>
      </div>
</template>

<script>
export default {
  name: "TaskAdd",
  props: ["categoryId"],
  data() {
    return {
      show: true,
      title: ""
    }
  },
  methods: {
    createNewTask(id){
      const dataTask = { CategoryId: id, title:this.title }
      this.$emit("newDataTask", dataTask)
      this.removeAddForm()
    },
    removeAddForm(){
      this.show = false
      this.title = ""
    }
  }
}
</script>

<style>

</style>