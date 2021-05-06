<template>
  <div class="filters">
    <input
      type="text"
      id="myInput"
      onkeyup="filterFunction()"
      placeholder="Search for names.."
      style="margin-top: 0px;"
    />
    <br />
    <label for="filterSex">Filter Sex:</label>
    <select
      id="filterSex"
      required
      class="styled-input"
      onchange="filterFunction()"
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
export default {
  name: "Filters",
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
