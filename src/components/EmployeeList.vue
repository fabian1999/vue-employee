<template>
  <div class="list">
    <table id="table">
      <tr>
        <th>Last Name</th>
        <th>First Name</th>
        <th>Email</th>
        <th>Sex</th>
        <th>Date</th>
        <th>Image</th>
        <th>Delete</th>
      </tr>
    </table>
  </div>
</template>

<script>
import $ from "jquery";

export default {
  name: "EmployeeList",
  data() {
    return {
      employeesList: [],
    };
  },
  async created() {
    let self = this;
    $.ajax({
      method: "GET",
      url: "https://localhost:5001/employee/Employee",
      success: function(data) {
        this.employeesList = data;
        self.loadEmployees(this.employeesList);
      },
      error: function() {
        alert(`Failed to get employees list.`);
      },
    });
  },
  methods: {
    loadEmployees(employeesList) {
      for (var index = 0; index < employeesList.length; index++) {
        this.appendRow(employeesList[index]);
      }
    },
    appendRow(employee) {
      let employeesTable = document.getElementById("table");
      var id = employeesTable.getElementsByTagName("tr").length;

      employeesTable.innerHTML += `<tr><td>
        ${employee.lastName}
        </td><td>
        ${employee.firstName}
        </td><td>
        ${employee.email}
        </td><td>
        ${employee.gender}
        </td><td>
        ${employee.birthdate}
        </td><td>
        <img id='image" ${id} 'style='width: 20px; height: 20px' src='#'></img></td><td><button onClick='this.deleteUser(this, ${employee.id})'>X</button></td></tr>`;
    },
    deleteUser(btn, idFromDb) {
      var row = btn.parentNode.parentNode;
      row.parentNode.removeChild(row);

      $.ajax({
        method: "DELETE",
        url: `https://localhost:5001/employee/Employee/${idFromDb}`,
        success: function() {},
        error: function() {
          alert(`Failed to delete employee.`);
        },
      });
    },
  },
};
</script>

<style scoped>
#table {
  width: 120vh;
}

.list {
  width: 130vh;
  height: 80vh;
  background-color: white;
  display: grid;
  justify-content: center;
  border-radius: 10px;
  box-shadow: 5px 5px 5px 1px #000000;
}

td {
  text-align: center;
}
</style>
