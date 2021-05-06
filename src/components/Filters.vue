<template>
  <div class="filters">
    <input
      type="text"
      id="myInput"
      @keyup="filterFunction()"
      placeholder="Search for names.."
      style="margin-top: 0px;"
    />
    <br />
    <label for="filterSex">Filter Sex:</label>
    <select
      id="filterSex"
      required
      class="styled-input"
      @change="filterFunction()"
      style="margin-bottom: 10px;"
    >
      <option value="" selected="selected">None</option>
      <option value="Barbat">Barbat</option>
      <option value="Femeie">Femeie</option>
    </select>
    <br />
    <button
      class="styled-buttons"
      id="sortDateButton"
      sort="up"
      onClick="sortTableByDate()"
      style="margin-bottom: 0; height: 25px;"
    >
      Sort By Date
    </button>
  </div>
</template>

<script>
import $ from "jquery";

export default {
  name: "Filters",
  props: {
      employeeTable: HTMLTableElement,
  },
  methods: {
    filterFunction() {
      var filter = $("#filterSex").val();
      var table = this.employeeTable;
      var tr = table.getElementsByTagName("tr");

      var input = document.getElementById("myInput");
      var filterInput = input.value.toUpperCase();

      for (var i = 0; i < tr.length; i++) {
        var td = tr[i].getElementsByTagName("td")[3];
        var td0 = tr[i].getElementsByTagName("td")[0];
        if (td && td0) {
          var txtValue = td.textContent || td.innerText;
          var txtValue0 = td0.textContent || td0.innerText;
          if (
            txtValue.indexOf(filter) > -1 &&
            txtValue0.toUpperCase().indexOf(filterInput) > -1
          ) {
            tr[i].style.display = "";
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    },
  },
};
</script>

<style scoped>
.filters {
  margin: auto;
  width: 50%;
  padding: 10px;
}

#myInput {
  background-position: 10px 12px; /* Position the search icon */
  background-repeat: no-repeat; /* Do not repeat the icon image */
  width: 98vh; /* Full-width */
  font-size: 16px; /* Increase font-size */
  padding: 12px 20px 12px 40px; /* Add some padding */
  border: 1px solid #ddd; /* Add a grey border */
  margin-top: 12px; /* Add some space below the input */
  height: 20px;
  border-radius: 20px;
  margin-bottom: 10px;
}

#myInput:focus {
  outline: none;
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
</style>
