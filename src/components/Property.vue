<template>
<div class="comp">
  <StringValue ref="keyInput" v-model="internalState.key" @input="updateValue()" />
  <span> : </span>
  <Value ref="valueInput" v-model="internalState.value" @input="updateValue()"/>
</div>
</template>
<script>

export default {
  name: "Property",
  props: {
    value: Object
  },
  watch: {
    value: function(newVal) { // next argument can be oldVal if necessary
      // TODO do input validation here
      this.internalState = newVal;
    }
  },
  data: function() {
    return {
      internalState: {
        key: "",
        value: ""
      }
    }
  },
  methods: {
    updateValue: function() {
      this.$emit('input', this.internalState);
    }
  },
  mounted: function() {
    this.internalState = this.value;
  }
};
</script>

<style scoped>

</style>
