<template>
  <div class="container mt-5">
  <label class="text-reader">
    <button class="btn btn-light" @click="seen = !seen">
      <input class="form-control" accept="text/plain" type="file" @change="loadFile">
    </button>
      <p class="text-danger">Yalnızca txt uzantılı dosyalar seçilebilir!</p>
  </label>
</div>
</template>
<script>
export default {
    data: () =>
    ({
    seen: false
    }),
  methods: {
    loadFile(ev) {
      const file = ev.target.files[0];
      const reader = new FileReader();
      reader.onload = e => this.$emit("onLoaded", e.target.result);
      reader.readAsText(file);
    }
  },
}
</script>