<template>
  <div class="container">
    <h2 class="text-center mt-5">Aplikasi ToDoList Vue.js</h2>

    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        class="form-control rounded-0"
        Placeholder="Masukan Tugas"
        name=""
        id=""
      />
      <button @click="submitTask" class="btn btn-warning rounded-0">
        Kirim
      </button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td style="width: 120px">
            <span @click="changeStatus(index)" class="pointer">
              {{ task.status }}
            </span>
          </td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },

  data() {
    return {
      task: "",
      editedTask: null,
      availableStatuses: ["Start", "Progress", "Finish"],
      tasks: [
        {
          name: "Ngoding ",
          status: "Start",
        },
        {
          name: "Makan Nasi Padang",
          status: "Progress",
        },
      ],
    };
  },

  methods: {
    submitTask() {
      if (this.task.length === 0) return;

      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "to-do",
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = "";
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index) {
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);

      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    },

    // firstCharUpper(str) {
    //   return str.chartAt(0).toUpperCase() + str.slice(1);
    // },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>

