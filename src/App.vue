<template>
  <Filters :employeeTable="employeeTable"/>
  <div class="form-container">
    <Form @addEmployee="addNewEmployee"/>
    <EmployeeList @tableOfEmployees="onTableOfEmployeesClick" ref="employees"/>
  </div>
</template>

<script>
import Filters from "./components/Filters.vue";
import Form from "./components/Form.vue";
import EmployeeList from "./components/EmployeeList.vue";

export default {
  name: "App",
  components: {
    Filters,
    Form,
    EmployeeList,
  },
  data() {
    return {
      employeeTable: HTMLTableElement
    }
  },
  methods: {
    addNewEmployee: function(data){
      this.$refs.employees.appendRow(data);
    },
    onTableOfEmployeesClick: function(value){
      this.employeeTable = value;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

body,
html {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  background-color: #eeeeee;
}

@media only screen and (max-width: 1200px) {
  body,
  html {
    overflow: auto;
  }
}

.form-container {
  width: 92%;
  margin-left: 8%;
  margin-top: 0%;
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

.styled-buttons:hover {
  box-shadow: 0px 0px 1px 1px #000000;
}
</style>
