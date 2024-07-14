<script>
  let currentdate = new Date();
  let datetime = "";
  function updateDate() {
    currentdate = new Date();
    datetime =
      currentdate.getDate() +
      "/" +
      (currentdate.getMonth() + 1) +
      "/" +
      currentdate.getFullYear() +
      " " +
      String(currentdate.getHours()).padStart(2, "0") +
      ":" +
      String(currentdate.getMinutes()).padStart(2, "0") +
      ":" +
      String(currentdate.getSeconds()).padStart(2, "0");
  }
</script>

<p on:mouseenter={updateDate}>
  Date is {datetime}
</p>
