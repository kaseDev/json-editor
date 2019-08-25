<template>
  <div id='comp'>
    <draggable v-model="internalRepresentation" @end="onEnd" handle=".handle">
      <span v-for="(internal, index) in internalRepresentation" :key="index" :index="index">
        <span class="handle">&#9552;</span>
        <span id="remove-value-button" @click="removeValue(index)">x</span>
        <Value
            v-model="internalRepresentation[index]"
            @input="updateValue"
        ></Value>
        <br>
      </span>
    </draggable>
    <button @click="addValue">Add Value</button>
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: "Array",
  components: {
    draggable
  },
  data: function() {
    return {
      internalRepresentation: [],
      oldIndex: "",
      newIndex: ""
    }
  },
  methods: {
    addValue: function() {
      this.internalRepresentation.push(null);
      this.updateValue();
    },
    removeValue: function(index) {
      this.internalRepresentation.splice(index, 1);
      this.updateValue();
    },
    onEnd: function(evnt) {
      this.oldIndex = evnt.oldIndex;
      this.newIndex = evnt.newIndex;
      this.updateValue();
    },
    updateValue: function() {
      this.$emit('input', this.internalRepresentation);
    }
  },
  props: {
    value: Array
  },
  watch: {
    value: function(newVal) {
      this.internalValue = newVal;
    }
  },
  mounted: function() {
    this.internalValue = this.value;
  }
}
</script>

<style scoped>
#comp {
  border: black solid 1px;
}

#remove-value-button {
  border: black solid 1px;
  background: lightgray;
  margin: 3px;
  padding: 0 3px 0 3px;
}
</style>
