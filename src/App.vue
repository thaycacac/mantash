<template>
  <b-container>
    <b-row class="mt-5">
      <b-col>
        <add-task @addTask="addTask" />
      </b-col>
      <b-col>
        <view-task />
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
      console.log(this.tasks);
      this.saveData();
    },
    saveData() {
      localStorage.setItem("data", JSON.stringify(this.tasks));
    },
  },
};
</script>

<style lang="scss">
</style>
