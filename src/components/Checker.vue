<template>
  <div class="container">
    <p>{{messageLength}}文字</p>
    <textarea v-model="message"></textarea>
    <div>
      <input type="checkbox" id="checkbox" v-model="checked" />
      <label for="checkbox">{{label}}を含める</label>
    </div>
    <button v-on:click="copy">コピー</button>
  </div>
</template>

<script>
import { text } from "body-parser";
export default {
  name: "Checker",
  data: function() {
    return {
      checked: false,
      message: ""
    };
  },

  computed: {
    label: function() {
      return `（${this.messageLength}字）`;
    },
    messageLength: function() {
      const unit = 3; //(字)の部分の長さ
      const digits = (this.message.length + unit).toString(10).length;
      return this.message.length + (this.checked ? unit + digits : 0);
    }
  },
  methods: {
    copy: function(event) {
      const textarea = document.createElement("textarea");
      textarea.textContent = this.message + this.label;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand("copy");
      document.body.removeChild(textarea);
      alert("クリップボードにコピーしました");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 100vw;
  height: 100vh;
}

textarea {
  width: 80%;
  height: 50%;
  font-size: 2rem;
}
</style>
