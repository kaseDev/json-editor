<template>
<div class="comp">
  <Value ref="keyInput" plText="key" v-model="internalState.key" @input="updateValue()" />
  <span>:</span>
  <Value ref="valueInput" plText="value" v-model="internalState.value" @input="updateValue()"/>
</div>
</template>
<script>
import Value from './Value.vue';

export default {
  name: "Property",
  components: {
    Value
  },
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
