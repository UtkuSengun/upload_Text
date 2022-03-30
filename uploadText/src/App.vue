<template>
  <div id="app">
		<text-read @loading="text = $event"></text-read>
    <br>
    <div class="container">
      <textarea class="form-control"  style="height: 500px"  v-model="text"></textarea>
    </div>
  </div>
</template>
<script>
import TextRead from "./components/TextRead.vue";

export default {
  name: "app",
  data: () => ({ text: "" }),
  components: {
    TextRead
  }
};
</script>

