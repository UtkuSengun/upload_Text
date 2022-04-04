<template>
  <div id="app">
    <text-read @onLoaded="handleTextLoaded"></text-read>
    <br />
    <div class="container">
      <textarea
        class="form-control"
        style="height: 300px"
        v-model="text"
      ></textarea>
      <div class="row m-3">
        <div class="col-5">
          <input
            class="form-control form-control-sm"
            type="text"
            placeholder="Aranan"
            v-model="searchKeyword"
          />
        </div>
        <div class="col-5">
          <input
            class="form-control form-control-sm border-left"
            type="text"
            placeholder="Güncellenecek"
            v-model="replaceKeyword"
          />
        </div>
        <div class="col-2 text-center">
          <button
            type="button"
            class="btn btn-success btn-sm px-5 fw-bold"
            @click="handleReplaceText"
          >
            Değiştir
          </button>
        </div>
      </div>
      <table class="table table-hover text-center">
        <thead>
          <tr>
            <th scope="col">Tarih</th>
            <th scope="col">Aranan</th>
            <th scope="col">Değişen</th>
            <th scope="col">Etkilenen</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(log, index) in logSearchData" v-bind:key="index">
            <th scope="row">{{ log.dataTime }}</th>
            <td>{{ log.searchKeyword }}</td>
            <td>{{ log.replaceKeyword }}</td>
            <td>{{ log.searchKeyword }} - {{ log.replaceKeyword }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import TextRead from "./components/TextRead.vue";
export default {
  name: "app",
  data() {
    return {
      text: "",
      searchKeyword: "",
      replaceKeyword: "",
      logSearchData: []
    };
  },
  components: {
    TextRead
  },
  methods: {
    handleTextLoaded(text) {
      this.text = text;
    },
    handleReplaceText() {
      let currentText = this.text;
      this.text = currentText.replaceAll(
        this.searchKeyword,
        this.replaceKeyword
      );

      if (!this.replaceKeyword) return;

      var items = {
        searchKeyword: this.searchKeyword,
        replaceKeyword: this.replaceKeyword,
        dataTime: new Date()
          .toJSON()
          .slice(0, 10)
          .replace(/-/g, "/")
      };

      let logDataItems = JSON.parse(localStorage.getItem("logData")) || [];
      logDataItems.push(items);
      localStorage.setItem("logData", JSON.stringify(logDataItems));
      this.logSearchData.push(items);
    },
    saveText() {
      let parsed = JSON.stringify(this.text);
      localStorage.setItem("text", parsed);
    }
  },
  mounted() {
    if (localStorage.getItem("logData")) {
      this.logSearchData = JSON.parse(localStorage.getItem("logData"));
    }
  }
};
</script>
