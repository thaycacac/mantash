<template>
  <b-container>
    <b-row class="mt-5">
      <b-col>
        <add-task @addTask="addTask" />
      </b-col>
      <b-col>
        <view-task
          :tasks="tasks"
          @updateTask="updateTask"
          @deleteTask="deleteTask"
          @doneMultiple="doneMultiple"
          @deleteMultiple="deleteMultiple"
        />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import AddTask from "./components/AddTask";
import ViewTask from "./components/ViewTask";
export default {
  components: {
    AddTask,
    ViewTask,
  },
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem("data")) || [],
    };
  },
  methods: {
    addTask(data) {
      this.tasks.push({
        ...data,
        isComplete: false,
      });
      this.saveData();
    },
    updateTask(id, data) {
      const index = this.tasks.findIndex((item) => item.id === id);
      this.tasks[index] = data;
      this.saveData();
    },
    deleteTask(id) {
      const index = this.tasks.findIndex((item) => item.id === id);
      this.tasks.splice(index, 1);
      this.saveData();
    },
    saveData() {
      localStorage.setItem("data", JSON.stringify(this.tasks));
    },
    doneMultiple(list) {
      this.tasks.forEach((item, index) => {
        if (list.includes(item.id)) {
          this.tasks[index].isComplete = true;
        }
      });
      this.saveData();
    },
    deleteMultiple(list) {
      this.tasks.forEach((item, index) => {
        if (list.includes(item.id)) {
          this.tasks.splice(index, 1);
        }
      });
      this.saveData();
    },
  },
};
</script>

<style lang="scss">
</style>
