<template>
  <div id="app">
    <div class="label">加密前文本</div>
    <el-input
      type="textarea"
      placeholder="请输入加密前内容"
      @change="encode"
      :rows="config.rows"
      v-model="decodeText">
    </el-input>
    <div class="label">加密后文本</div>

    <el-input
      type="textarea"
      placeholder="请输入加密后内容"
      :rows="config.rows"
      @change="decode"
      v-model="encodeText">
    </el-input>
  </div>
</template>

<script>


  export default {
    name: 'App',
    data() {
      return {
        config: {
          rows: 10
        },
        encodeText: '',
        decodeText: '',
        scretKey: 'trubasa123'
      }
    },
    mounted() {

    },
    methods: {
      encode(text) {
        if (text) {
          this.encodeText = this.$cryptoJS.AES.encrypt(JSON.stringify(text), this.scretKey).toString();
        } else {
          this.encodeText = ''
        }
      },
      decode(text) {
        if (text) {
          var bytes = this.$cryptoJS.AES.decrypt(text, this.scretKey);
          this.decodeText = JSON.parse(bytes.toString(this.$cryptoJS.enc.Utf8));
        } else {
          this.decodeText = ''
        }
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    padding: 10px;
  }

  .label {
    padding: 10px 0;
  }
</style>
