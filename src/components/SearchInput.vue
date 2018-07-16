<template>
    <div class="search-wrapper">
      <label for="search">Search</label>
      <input
        type="search"
        id="search"
        :class="{ dark }"
        :value="value"
        @input="handleChange"
      />
    </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.search-wrapper {
  display: flex;
  flex-direction: column;
  width: 250px;
  margin: 50px 0 0 0;
  label {
    display: none;
  }
  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid #fff;
    background: none;
    text-align: center;
    color: #fff;
    font-size: 1.2rem;
    letter-spacing: 1px;
    transition: box-shadow 0.3s;
    &:focus {
      outline: none;
      box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.5);
    }
  }
  .dark {
    color: #1e3d4a;
    border-bottom-color: #1e3d4a;
    &:focus {
      box-shadow: 0 10px 20px -8px rgba(#1e3d4a, 0.5);
    }
  }
}
</style>
