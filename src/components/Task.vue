<template>
  <div class="col-sm my-2 mx-2 shadow rounded">
          <div class="card">
            <div class="card-body">
              <p class="card-text">
                {{ dataTask.title }}
              </p>
              <p><small class="text-muted">This line of text is meant to be treated as fine print.</small></p>
              <div class="col">
                <button type="button" class="btn btn-primary btn-sm shadow rounded">Small button</button>
                <button type="button" class="btn btn-primary btn-sm shadow rounded"><i class="bi bi-gear"></i></button>
                <button type="button" class="btn btn-primary btn-sm shadow rounded"><i class="bi bi-gear"></i></button>
              </div>
            </div>
          </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: [
    "dataTask"
  ],
  data() {
    return {}
  },
  // created(){
  //   console.log(this.dataTask);
  // }
}
</script>

<style>

</style>