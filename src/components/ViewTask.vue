<template>
  <div>
    <b-form-input
      required
      v-model="textSearch"
      placeholder="Search..."
      @keypress.enter="searchTask"
    ></b-form-input>
    <b-card class="my-2" v-for="(item, index) in tasksTemp" :key="index">
      <div class="d-flex justify-content-between">
        <b-form-checkbox
          v-model="item.isSelected"
          name="checkbox-1"
          :value="true"
          :unchecked-value="false"
        >{{ item.title }}</b-form-checkbox>
        <div>
          <b-button variant="primary" class="mr-2" @click="detail(item.id)">Detail</b-button>
          <b-button variant="danger" @click="deleteTask(item.id)">Delete</b-button>
        </div>
      </div>
      <div class="mt-3" v-if="item.id === idSelected">
        <b-form-input required v-model="taskUpdate.title" placeholder="Add new task..."></b-form-input>
        <b-form-textarea
          class="mt-3"
          v-model="taskUpdate.description"
          placeholder="Enter description..."
          rows="3"
          max-rows="6"
        ></b-form-textarea>
        <div class="d-flex mt-3">
          <b-form-datepicker v-model="taskUpdate.dueDate" :min="min"></b-form-datepicker>
          <b-form-select v-model="taskUpdate.piority" :options="options" class="ml-1"></b-form-select>
        </div>
        <b-button class="mt-3" variant="success" block type="submit" @click="update(item.id)">Update</b-button>
      </div>
    </b-card>
    <b-card class="my-2 action">
      <div class="d-flex justify-content-between align-items-center">
        <p class="text">Bulk Action</p>
        <div>
          <b-button variant="primary" class="mr-2" @click="doneMultiple()">Done</b-button>
          <b-button variant="danger" @click="deleteMultiple()">Delete</b-button>
        </div>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true,
      default: function () {
        return [];
      },
    },
  },
  data() {
    const temp = this.tasks
      .filter((item) => item.isComplete === false)
      .sort(
        (a, b) => new Date(a.dueDate).getTime() - new Date(b.dueDate).getTime()
      );
    return {
      idSelected: "",
      textSearch: "",
      min: new Date(),
      options: [
        { value: "low", text: "Low" },
        { value: "normal", text: "Normal " },
        { value: "high", text: "High" },
      ],
      tasksTemp: temp,
      taskUpdate: {
        title: "",
        description: "",
        dueDate: new Date(),
        piority: "normal",
        isComplete: false,
      },
    };
  },
  watch: {
    tasks: function (val) {
      this.tasksTemp = val
        .filter((item) => item.isComplete === false)
        .sort(
          (a, b) =>
            new Date(a.dueDate).getTime() - new Date(b.dueDate).getTime()
        );
    },
  },
  methods: {
    detail(id) {
      this.idSelected === id ? (this.idSelected = "") : (this.idSelected = id);
      this.taskUpdate = this.tasks.find((item) => item.id === id);
    },
    update(id) {
      this.$emit("updateTask", id, this.taskUpdate);
      this.idSelected = false;
    },
    deleteTask(id) {
      this.$emit("deleteTask", id);
    },
    searchTask() {
      this.tasksTemp = this.tasks
        .filter((item) => {
          return (
            item.isComplete === false &&
            item.title.toLowerCase().includes(this.textSearch.toLowerCase())
          );
        })
        .sort(
          (a, b) =>
            new Date(a.dueDate).getTime() - new Date(b.dueDate).getTime()
        );
    },
    doneMultiple() {
      const listSelected = this.tasksTemp.filter(
        (item) => item.isSelected === true
      );
      const listIdSelected = listSelected.map((item) => item.id);
      this.$emit("doneMultiple", listIdSelected);
      this.tasksTemp = this.tasksTemp.map((item) => {
        if (listIdSelected.includes(item.id)) {
          item.isComplete = true;
        }
        return item;
      });
      this.tasksTemp = this.tasksTemp.filter(
        (item) => item.isComplete === false
      );
    },
    deleteMultiple() {
      const listSelected = this.tasksTemp.filter(
        (item) => item.isSelected === true
      );
      this.$emit(
        "deleteMultiple",
        listSelected.map((item) => item.id)
      );
    },
  },
};
</script>

<style lang="scss">
.action {
  background: #d2d2d2 !important;
  .text {
    margin: 0;
  }
}
</style>