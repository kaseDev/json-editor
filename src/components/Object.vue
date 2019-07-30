<template>
  <div id="comp">
    <span v-for="(internal, index) in internalProperties" :key="index" :index="index">
      <span id="remove-property-button" @click="removeProperty(index)">x</span>
      <Property
          :value="internal"
          v-model="internalProperties[index]"
          @input="updateValue"
      ></Property>
      <br>
    </span>
    <button @click="addProperty">Add Property</button>
  </div>
</template>

<script>
export default {
  name: "Object",
  data: function() {
    return {
      internalProperties: []
    }
  },
  methods: {
    updateValue: function() {
      this.$emit('input', this.restructureObject(this.internalProperties));
    },
    addProperty: function() {
      this.internalProperties.push({
        'key' : 'key',
        'value': 'value'
      });
    },
    removeProperty: function(index) {
      this.internalProperties.splice(index, 1);
    },
    destructureObject: function(obj) {
      const properties = [];
      const entries = Object.entries(obj);
      for (const [key, value] of entries) {
        let property = {
          'key' : key,
          'value' : value
        };
        properties.push(property);
      }
      return properties;
    },
    restructureObject: function(properties) {
      const obj = {};
      for (const property of properties)
        obj[property["key"]] = property["value"];
      return obj;
    }
  },
  props: {
    // value: Array,
    value: Object
  },
  watch: {
    value: function(newVal) {
      // console.log(newVal);
      this.internalProperties = this.destructureObject(newVal);
    }
  },
  mounted: function() {
    this.internalProperties = this.destructureObject(this.value);
  }
}
</script>

<style scoped>
#comp {
  border: black solid 1px;
}

#remove-property-button {
  border: black solid 1px;
  background: lightgray;
  margin: 3px;
  padding: 0 3px 0 3px;
}
</style>
