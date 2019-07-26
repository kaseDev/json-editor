<template>
<span class="comp">
  <span v-if="isNull && isVacant">null</span>
  <StringValue v-else-if="isString" v-model="internalValue" @input="updateValue"/>
  <Object v-else-if="isObject" v-model="internalValue" @input="updateValue"/>

  <select v-if="isFilling" ref="select" @blur="failedToFill" @input="filledType">
    <option disabled selected value> -- select an option -- </option>
    <option v-for="option in typeOptions.slice(1)" :key="option" :value="option">{{ option }}</option>
  </select>
  <button v-else-if="isVacant" @click="tryToFill" tabindex="-1" @input="updateValue">+</button>
  <button v-else-if="isFilled" @click="vacate" tabindex="-1" @input="updateValue">x</button>

  <!-- <span>
    <span>internalValue: {{internalValue}} </span> ||
    <span>valueType: {{valueType}} </span> ||
    <span>interfaceState: {{interfaceState}} </span>
  </span> -->
</span>
</template>

<script>
export default {
  name: "Value",
  props: ['value'],
  watch: {
    value: function(newVal) {
      this.internalValue = newVal;
      this.initalizeFromInternalValue();
    }
  },
  data: function() {
    return {
      internalValue: null,
      valueType: "null",
      interfaceState: "vacant",
      typeOptions: [
        "null",
        "string",
        "object",
      ],
      interfaceStateOptions: [
        "vacant",
        "filling",
        "filled"
      ]
    };
  },
  methods: {
    updateValue: function() {
        this.$emit("input", this.internalValue);
    },
    vacate: function() {
      this.internalValue = null;
      this.valueType = this.typeOptions[0];
      this.interfaceState = this.interfaceStateOptions[0];
      this.updateValue();
    },
    tryToFill: function() {
      this.interfaceState = this.interfaceStateOptions[1];
      this.$nextTick(() => this.$refs.select.focus());
    },
    filledType: function() {
      console.log(this.interfaceState + " -> " + this.interfaceStateOptions[2]);
      this.interfaceState = this.interfaceStateOptions[2];
      this.valueType = this.$refs.select.options[this.$refs.select.selectedIndex].value;
      this.initializeInternalValue();
      this.updateValue();
    },
    failedToFill: function() {
      if (this.interfaceState !== "filled")
        this.interfaceState = this.interfaceStateOptions[0];
    },
    initializeInternalValue: function() {
      switch (this.valueType) {
        case "null":
          this.internalValue = null;
          break;
        case "string":
          this.internalValue = '';
          break;
        case "object":
          this.internalValue = {innerKey: "Jane Doe"};
          break;
      }
    },
    initalizeFromInternalValue: function() {
      if (this.internalValue === null) {
        this.valueType = "null";
        this.interfaceState = this.interfaceStateOptions[0];
      } else {
        this.valueType = (typeof this.internalValue);
        this.interfaceState = this.interfaceStateOptions[2];
      }
    }
  },
  computed: {
    isNull: function() {
      return this.valueType === this.typeOptions[0];
    },
    isString: function() {
      return this.valueType === this.typeOptions[1];
    },
    isObject: function() {
      return this.valueType === this.typeOptions[2];
    },
    isVacant: function() {
      return this.interfaceState === this.interfaceStateOptions[0];
    },
    isFilling: function() {
      return this.interfaceState === this.interfaceStateOptions[1];
    },
    isFilled: function() {
      return this.interfaceState === this.interfaceStateOptions[2];
    }

  },
  mounted: function() {
    this.internalValue = this.value;
    this.initalizeFromInternalValue();
  }
};
</script>

<style scoped>

</style>
