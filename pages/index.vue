<template>
  <div class="container">

    <div class="row">
      <div class="col lg 12 text-center">
        <h3 class="page-title">Todo List</h3>
      </div>
      <div class="col-lg-12" mt-10>
        <form action="#" method="POST" enctype="multipart/form">
          <!-- go to the store class on TodoController using web.php route  -->

          <!-- for the token -->
          <div class="row">
            <div class="col-lg-8">
              <div class="form-group">
                <input class="form-control" name="title" type="text" placeholder="Enter task" required>
              </div>
            </div>
            <div class="col-lg-4">
              <button class="btn btn-primary">Submit</button>
            </div>

          </div>
        </form>
      </div>
      <div class="col-lg-12 mt-5">
        <div>
          <table class="table table-striped table-hover caption-top">
            <caption>Todos list</caption>
            <thead class="table-dark">
              <tr>
                <th scope="col">No</th>
                <th scope="col">Title</th>
                <th scope="col">Status</th>
                <th scope="col">Action</th>

              </tr>
            </thead>
            <tbody>
              <tr v-for="task in tasks" :key="task.id">
                <th scope="row">{{ task.id }}</th>
                <td>{{ task.title }}</td>
                <td>

                  <span v-if="task.done == 0" class="badge bg-warning">Not Completed</span>

                  <span v-if="task.done == 1" class="badge bg-success">Completed </span>

                </td>

                <td>
                  <button class="btn btn-primary">edit<i class="fa-solid fa-pen"></i></button>
                  <button class="btn btn-success"> done<i class="fa-solid fa-circle-check"></i></button>
                  <button class="btn btn-danger"> delete<i class="fa-solid fa-trash"></i></button>
                  <button class="btn btn-warning"> sub tasks<i class="fa-solid fa-list-check"></i></button>
                </td>
              </tr>
              <tr v-if="tasks.length == 0">
                <td colspan="4" class="text-center">No data found</td>
              </tr>



            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

</template>



<script>
export default {
  name: 'home',
  layout: 'dashboard',
  data() {
    return {
      tasks: []
    }
  },
  mounted() {
    this.getTasks()
  },

  methods: {
    getTasks() {
      this.$axios.get('api/tasks')
        .then(response => {
          this.tasks = response.data;
          console.log(this.tasks);

        })
        .catch(error => {
          console.log(error)
        })
    }

  },

  mounted() {
    this.getTasks();
  }

}
</script>



<style>
.page-title {
  padding-top: 10vh;
  padding-bottom: 3vh;

  font-size: 40px;
  font-weight: 400;
  align-content: center;
  color: blue;
}
</style>
