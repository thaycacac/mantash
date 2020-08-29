<template>
  <div>
    <b-card title="New Task" class="mb-2" align="center">
      <b-form @submit.prevent="submit">
        <b-form-input required v-model="title" placeholder="Add new task..."></b-form-input>
        <b-form-textarea
          class="mt-3"
          v-model="description"
          placeholder="Enter description..."
          rows="3"
          max-rows="6"
        ></b-form-textarea>
        <div class="d-flex mt-3">
          <b-form-datepicker v-model="dueDate" :min="min"></b-form-datepicker>
          <b-form-select v-model="piority" :options="options" class="ml-1"></b-form-select>
        </div>
        <b-button class="mt-3" variant="success" block type="submit">Add</b-button>
      </b-form>
    </b-card>
  </div>
</template>

<script>
import { id } from "../utils/index";
export default {
  data() {
    return {
      title: "",
      description: "",
      dueDate: new Date(),
      min: new Date(),
      piority: "normal",
      options: [
        { value: "low", text: "Low" },
        { value: "normal", text: "Normal " },
        { value: "high", text: "High" },
      ],
    };
  },
  methods: {
    submit() {
      this.$emit("addTask", {
        id: id(),
        title: this.title,
        description: this.description,
        dueDate: this.dueDate,
        piority: this.piority,
      });
      this.clearData();
    },
    clearData() {
      this.title = "";
      this.description = "";
      this.dueDate = new Date();
      this.piority = "normal";
    },
  },
};
</script>

