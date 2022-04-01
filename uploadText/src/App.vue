<template>
  <div id="app">
		<text-read @onLoaded="handleTextLoaded"></text-read>
    <br>
    <div class="container">
      <textarea class="form-control"  style="height: 300px"  v-model="text"></textarea>
    <div class="row m-3">
        <div class="col-5">
            <input class="form-control form-control-sm" type="text" placeholder="Aranan" v-model="searchKeyword">
        </div>
        <div class="col-5">
            <input class="form-control form-control-sm border-left" type="text" placeholder="Güncellenecek" v-model="replaceKeyword">
        </div>
        <div class="col-2 text-center">
            <button type="button" class="btn btn-success btn-sm px-5 fw-bold" @click="handleReplaceText">Değiştir</button>
        </div>
    </div>
    </div>
  </div>
</template>
<script>
import TextRead from "./components/TextRead.vue";
export default {
  name: "app",
  data () {
    return {
      text: "",
      searchKeyword: "",
      replaceKeyword: ""
    }
  },
  components: {
    TextRead,
  },
  methods: {
    handleTextLoaded(text) {
      this.text=text
    },
    handleReplaceText(){
      let currentText = this.text;
      this.text = currentText.replaceAll(this.searchKeyword,this.replaceKeyword)
    }
  }
};
</script>

