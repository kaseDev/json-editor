<template>
  <div id="comp">
    <!-- <Property v-for="i in internalProperties" :key="internalProperties[i].key" v-model="internalProperties[i]" /> -->
    <!-- <p v-for="i in internalProperties.length">{{ i }}</p> -->
    <!-- <Property v-model="fieldTest" /> -->
    <!-- <p>{{fieldTest}}</p> -->
    <Property
        v-for="(internal, index) in internalProperties"
        :value="internal"
        :index="index"
        :key="index"
        v-model="internalProperties[index]"
        @input="updateValue()"
    ></Property>
    {{internalProperties}}
  </div>
</template>

<script>
import Property from './Property.vue';
export default {
  name: "Object",
  components: {
    Property
  },
  data: function() {
    return {
      internalProperties: []
    }
  },
  methods: {
    updateValue: function() {
      this.$emit('input', this.restructureObject(this.internalProperties));
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

<style>
</style>
