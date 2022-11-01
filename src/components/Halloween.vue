<template>
  <div>
    <h5>Halloween</h5>
  </div>
</template>

<script>
import axios from "axios";
export default {
  mounted() {
    axios.get("http://localhost:3000/account").then((res) => {
      console.log(res);
    });
  },
};
</script>
