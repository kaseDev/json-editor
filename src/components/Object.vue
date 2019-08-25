<template>
  <div id="comp">
    <draggable v-model="internalProperties" @end="onEnd" handle=".handle">
      <span v-for="(internal, index) in internalProperties" :key="index" :index="index">
        <span class="handle">&#9552;</span>
        <span id="remove-property-button" @click="removeProperty(index)">x</span>
        <Property
            :value="internal"
            v-model="internalProperties[index]"
            @input="updateValue"
        ></Property>
        <br>
      </span>
    </draggable>
    <button @click="addProperty">Add Property</button>
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: "Object",
  components: {
    draggable
  },
  data: function() {
    return {
      internalProperties: [],
      oldIndex: "",
      newIndex: ""
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
      this.updateValue();
    },
    removeProperty: function(index) {
      this.internalProperties.splice(index, 1);
      this.updateValue();
    },
    onEnd: function(evnt) {
      this.oldIndex = evnt.oldIndex;
      this.newIndex = evnt.newIndex;
      this.updateValue();
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
