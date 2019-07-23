<template>
<!-- <span class="comp"> -->
  <input type="text" :placeholder="plText" ref="textbox" v-model="internalValue" @input="updateValue()" />
<!-- </span> -->
</template>

<script>
export default {
  name: "Value",
  props: {
    value: String,
    plText: String
  },
  watch: {
    value: function(newVal) {
      // TODO do input validation here
      this.internalValue = newVal;
    }
  },
  data: function() {
    return {
      internalValue: ""
    };
  },
  methods: {
    updateValue: function() {
      // TODO do input validation here
      this.$emit("input", this.internalValue);
    }
  },
  mounted: function() {
    // TODO do input validation here
    this.internalValue = this.value;
  }
};
</script>

<style scoped>
#comp {
  display: inline;
  background: green;
}
</style>
