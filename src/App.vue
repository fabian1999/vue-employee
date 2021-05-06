<template>
  <Filters />
  <Form />
</template>

<script>
import Filters from "./components/Filters.vue";
import Form from "./components/Form.vue";

export default {
  name: "App",
  components: {
    Filters,
    Form
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.styled-buttons {
  height: 35px;
  width: 130px;
  margin: auto;
  margin-bottom: 20px;
  border: none;
  background-color: #f8f9fa;
  border-radius: 5px;
}
</style>
