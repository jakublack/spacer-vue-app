<template>  
    <div class="search-wrapper">
      <label for="search">Search</label>
      <input
        type="search"
        id="search"
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
    
</template>

<script>
export default {
  name: "SearchInput"
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
        }
    }

</style>
