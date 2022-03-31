<template>
  <div id="app">
		<text-read @loading="text = $event"></text-read>
    <br>
    <div class="container">
      <textarea class="form-control"  style="height: 300px"  v-model="text"></textarea>
    </div>
    <form-group></form-group>
  </div>
</template>
<script>
import TextRead from "./components/TextRead.vue";
import FormGroup from "./components/FormGroup.vue"

export default {
  name: "app",
  data: () => ({ text: "" }),
  components: {
    TextRead,
    FormGroup
  }
};
</script>

