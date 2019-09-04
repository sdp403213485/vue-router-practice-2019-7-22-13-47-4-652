<template>
  <div id="forms">
    <input type="text" v-model="inputtingText" />
    <button @click="handleAdd">Add</button>
  </div>
</template>
<script>
export default {
  name: "forms",
  data: function() {
    return {
      inputtingText: ""
    };
  },
  methods: {
    handleAdd: function() {
      this.$emit("addNewToDo", this.inputtingText);
      this.inputtingText = "";
    }
  }
};
</script>