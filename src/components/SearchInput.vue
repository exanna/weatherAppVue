<template>
  <input
    id="search"
    name="search"
    autocomplete="off"
    class="search"
    @input="handleChange"
    :value="value"
  />
</template>

<script>
export default {
  name: "SearchInput",
  props: {
    value: {
      type: String,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit("input", e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.search {
  z-index: 1;
  margin-top: 10px;
  border: none;
  border-bottom: 2px solid white;
  background-color: transparent;
  text-align: center;
  width: 200px;
  color: white;
  font-size: 20px;
  font-weight: 300;
  padding-bottom: 5px;
  font-family: "Montserrat", sans-serif;

  &:focus {
    outline: 0;
    box-shadow: 0 10px 10px -8px rgba(255, 255, 255, 0.5);
  }

  @media (min-width: 768px) {
    width: 400px;
    font-size: 24px;
  }
}
</style>
