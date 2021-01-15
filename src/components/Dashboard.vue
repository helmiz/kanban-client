<template>
   <div class="container-fluid" style="background-color: yellowgreen">
      <div class="row">
        
        <category v-for="category in categories" 
                  :key="category.id" 
                  :dataCategory="category"
                  @newDataTask="createTask"></category>

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
    createTask(payload){
      return this.$emit("addTask", payload)
    }
  }
}
</script>

<style>

</style>