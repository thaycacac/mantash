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
          v-model="item.isComplete"
          name="checkbox-1"
          :value="true"
          :unchecked-value="false"
        >{{ item.title }}</b-form-checkbox>
        <div>
          <b-button variant="primary" class="mr-2" @click="detail(item.id)">Detail</b-button>
          <b-button variant="danger" @click="deleteTask(index)">Delete</b-button>
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
        <b-button class="mt-3" variant="success" block type="submit" @click="update(index)">Update</b-button>
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
    return {
      idSelected: "",
      textSearch: "",
      min: new Date(),
      options: [
        { value: "low", text: "Low" },
        { value: "normal", text: "Normal " },
        { value: "high", text: "High" },
      ],
      tasksTemp: this.tasks,
      taskUpdate: {
        title: "",
        description: "",
        dueDate: new Date(),
        piority: "normal",
        isComplete: false,
      },
    };
  },
  methods: {
    detail(id) {
      this.idSelected === id ? (this.idSelected = "") : (this.idSelected = id);
      this.taskUpdate = this.tasks.find((item) => item.id === id);
    },
    update(index) {
      this.$emit("updateTask", index, {
        ...this.taskUpdate,
        ...this.tasksTemp[index].isComplete,
      });
      this.idSelected = false;
    },
    deleteTask(index) {
      this.$emit("deleteTask", index);
    },
    searchTask() {
      this.tasksTemp = this.tasks.filter((item) =>
        item.title.toLowerCase().includes(this.textSearch.toLowerCase())
      );
    },
  },
};
</script>