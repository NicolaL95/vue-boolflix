<template>
  <div id="header_container">
    <h1>BOOLFLIX</h1>
    <div class="input">
      <input
        v-model="customQuery"
        type="text"
        @keyup.enter="$emit('getQuery', customQuery), cleanInput()"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      customQuery: "",
    };
  },
  methods: {
    cleanInput() {
      this.customQuery = "";
    },
  },
};
</script>

<style lang="scss">
#header_container {
  background-color: black;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  padding: 5px 20px;
  h1 {
    color: #920000;
    font-size: 1.5rem;
    margin: 10px 0 5px;
  }
  .input {
    height: 25px;
    margin: 10px 0 5px;
  }
}
</style>