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
export default {
  name: "EmployeeList",
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
