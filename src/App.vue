<template>
  <div class="app">
    <h1>Is your string balanced?</h1>
    <input
      ref="input"
      type="text"
      v-model="string"
      placeholder="Type your string here..."
      required
    />
    <Balanced-string :string="string" />
  </div>
</template>

<script>
import BalancedString from "./components/BalancedString.vue";
export default {
  components: { BalancedString },
  name: "App",
  data() {
    return {
      string: null,
    };
  },
  mounted() {
    this.string = "";
    this.focusInput();
  },
  methods: {
    focusInput() {
      this.$refs.input.focus();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input {
  padding: 20px 30px;
  font-size: 14px;
  border-radius: 10px;
  border: 1px solid lightblue;
  width: 400px;
  margin: 20px auto;
}
</style>
