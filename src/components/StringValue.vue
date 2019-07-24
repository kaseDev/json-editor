<template>
  <div id="comp" :tabindex="focusable" @focus="enterEditMode">
    <h1>Hello</h1>
    <span class="quote" @dblclick="enterEditMode" v-show="whiteSpaceMode">"</span>
    <span v-if="!editMode" @dblclick="enterEditMode">{{ internalValue }}</span>
    <input v-else @blur="exitEditMode" @keyup.enter="exitEditMode" v-model="internalValue" type="test" ref='input' @input="fireInput"/>
    <span class="quote" @dblclick="enterEditMode" v-show="whiteSpaceMode">"</span>
  </div>
</template>

<script>
export default {
  name: "StringValue",
  props: {
    value: String
  },
  data: function() {
    return {
      internalValue: "",
      editMode: false
    }
  },
  watch: {
    value: function(newVal) {
      this.internalValue = newVal;
    }
  },
  methods: {
    enterEditMode: function() {
      this.editMode = true;
      this.$nextTick(() => this.$refs.input.focus());
    },
    exitEditMode: function() {
      this.editMode = false;
    },
    fireInput: function() {
      this.$emit("input", this.internalValue);
    }
  },
  computed: {
    whiteSpaceMode: function() {
      return !this.editMode && (this.internalValue === "" || /^\s|\s$/.test(this.internalValue));
    },
    focusable: function() {
      return (this.editMode) ? -1 : 0;
    }
  },
  mounted: function() {
    this.internalValue = this.value;
  }
}
</script>

<style>
  .quote {
    font-weight: bold;
  }
</style>
