<template>
  <div class="list">
    <table id="table">
      <thead>
        <tr>
          <th>Last Name</th>
          <th>First Name</th>
          <th>Email</th>
          <th>Sex</th>
          <th>Date</th>
          <th>Image</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody></tbody>
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
      this.$emit("tableOfEmployees", document.getElementById("table"));
    },
    async appendRow(data) {
      let tableNode = document.getElementById("table");
      const row = document.createElement("tr");
      row.style.cssText = "text-align:center";

      for (const key in data) {
        const cell = document.createElement("td");
        if (key === "id") {
          continue;
        }
        if (key === "birthdate") {
          cell.innerText = data[key].split("T")[0];
        } else {
          cell.innerText = data[key];
        }
        row.appendChild(cell);
      }
      if (tableNode.children.length < 2) {
        console.log("Table doesent contain body");
        return;
      }
      let button = document.createElement("button");
      button.innerHTML = "X";
      row.appendChild(button);
      button.onclick = function() {
        row.remove();
        $.ajax({
          method: "DELETE",
          url: `https://localhost:5001/employee/Employee/${data.id}`,
          error: function() {
            alert(`Failed to remove employee from list`);
          },
        });
      };
      tableNode.children[1].appendChild(row);
      this.employeesList.push(data);
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
