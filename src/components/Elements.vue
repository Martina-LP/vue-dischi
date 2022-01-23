<template>
  <div class="select">
    <select class="form-select form-select-lg mb-3"
      aria-label=".form-select-lg example"
      v-model="genreValue"
      @change="$emit('genreFilter', genreValue)">
      <option value="">Select a genre</option>
      <option value="Rock">Rock</option>
      <option value="Pop">Pop</option>
      <option value="Jazz">Jazz</option>
      <option value="Metal">Metal</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      genreValue: "",
    };
  },
};
</script>

<style scoped lang="scss">

</style>
