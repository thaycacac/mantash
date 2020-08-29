<template>
  <div>
    <b-form-input required v-model="textSearch" placeholder="Search..."></b-form-input>
    <b-card title="New Task" class="mb-2">
      <b-form-checkbox
        id="checkbox-1"
        v-model="hello"
        name="checkbox-1"
        :value="true"
        :unchecked-value="false"
      >Cộng hòa xã hội chủ nghĩa việt nam</b-form-checkbox>
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textSearch: "",
      hello: false,
    };
  },
};
</script>