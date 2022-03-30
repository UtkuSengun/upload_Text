<template>
<div class="container mt-5">
<label class="text-reader">
    <input class="form-control" accept="text/plain" type="file" @change="loadFile">
    <p class="text-danger">Yalnızca txt uzantılı dosyalar seçilebilir!</p>
  </label>
</div>
  

</template>

<script>
export default {
  methods: {
    loadFile(ev) {
      const file = ev.target.files[0];
      const reader = new FileReader();

      reader.onload = e => this.$emit("loading", e.target.result);
      reader.readAsText(file);
    }
  }
};
</script>