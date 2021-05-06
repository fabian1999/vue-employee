<template>
  <div class="form">
    <h1>Form</h1>

    <label for="lastName">Last Name:</label>
    <input
      type="text"
      id="lastName"
      name="lastName"
      value=""
      required
      class="styled-input"
    />

    <label for="firstName">First Name:</label>
    <input
      type="text"
      id="firstName"
      name="firstName"
      value=""
      required
      class="styled-input"
    />

    <label for="email">Email:</label>
    <input
      type="text"
      id="email"
      name="email"
      value=""
      required
      class="styled-input"
    />

    <label for="dropdown">Sex:</label>
    <select id="dropdown" required class="styled-input">
      <option value="" selected="selected">None</option>
      <option value="Barbat">Barbat</option>
      <option value="Femeie">Femeie</option>
    </select>

    <label class="label-start-date" for="start">Start date:</label>

    <input
      class="styled-input"
      type="date"
      id="start"
      name="trip-start"
      value=""
      min="2021-01-01"
      max="2022-12-31"
      required
    />

    <label for="myfile">Select files:</label>
    <input type="file" id="myfile" name="myfile" multiple />

    <button class="styled-buttons" @click="addFields()">Submit</button>
  </div>
</template>

<script>
import $ from "jquery";

export default {
  name: "Form",
  methods: {
    validateInput(newEmployee) {
      if (
        !newEmployee.firstName ||
        !newEmployee.lastName ||
        !newEmployee.email ||
        !newEmployee.birthdate
      ) {
        return false;
      }
      return true;
    },
    addFields() {
      var self = this;
      // Number of inputs to create
      var newEmployee = new Object();
      newEmployee.lastName = document.getElementById("lastName").value;
      newEmployee.firstName = document.getElementById("firstName").value;
      newEmployee.email = document.getElementById("email").value;
      newEmployee.gender = document.getElementById("dropdown").value;
      //newEmployee.file = document.getElementById("myfile");
      newEmployee.birthdate = document.getElementById("start").value;

      if (!this.validateInput(newEmployee)) {
        alert("Fields are required.");
      }

      $.ajax({
        method: "POST",
        contentType: "application/json",
        data: JSON.stringify(newEmployee),
        url: "https://localhost:5001/employee/Employee",
        success: function(data) {
            self.$emit('addEmployee', data);
        },
        error: function() {
          alert(`Failed to add employee.`);
        },
      });
    },
  },
};
</script>

<style scoped>
.form {
  width: 50vh;
  height: 80vh;
  display: grid;
  justify-content: center;
  background: #74ebd5; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #acb6e5,
    #74ebd5
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #acb6e5,
    #74ebd5
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  border-radius: 10px;
  box-shadow: -5px 5px 5px 1px rgba(0, 0, 0, 0.85);
  float: left;
}

#myfile {
  margin-bottom: 10px;
}

.styled-input {
  margin-bottom: 20px;
  border-radius: 10px;
  outline: none;
  border: none;
  box-shadow: 0px 0px 1px 1px #000000;
  padding-left: 10px;
  padding-right: 10px;
}

#dropdown {
  border-radius: 10px;
  outline: none;
  border: none;
  box-shadow: 0px 0px 1px 1px #000000;
  padding-left: 10px;
  padding-right: 10px;
}

.label-start-date {
  margin-top: 10px;
}
</style>
