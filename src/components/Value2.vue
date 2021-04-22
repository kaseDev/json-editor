<template>
<span class="comp">
    <StringValue v-if="internalValue === 'A'" v-model="stringValue" />
    <Object v-else-if="internalValue === 'B'" v-model="objectValue" />
    <Array v-else-if="internalValue === 'C'" v-model="arrayValue" />
</span>
</template>

<script>
export default {
  name: "Value",
  props: ['value'],
  watch: {
    value: function(newVal) {
      this.internalValue = newVal;
    }
  },
  data: function() {
    return {
      internalValue: null,
      stringValue: "string",
      objectValue: { "key": "objectValue", "second": "prop" },
      arrayValue: ["Array Value", ""]
    };
  },
  methods: {

  },
  mounted: function() {
    this.internalValue = this.value;
  }
};
</script>

<style scoped>
.tab {
  margin-left: 40px;
}
</style>
