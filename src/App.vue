<template>
  <div id="app">
    <Value2 v-model="value2Test" />
  </div>
</template>

<script>
import Vue from 'vue';
import StringValue from "./components/StringValue.vue";
import Value from "./components/Value.vue";
import Value2 from "./components/Value2.vue";
import Property from "./components/Property.vue";
import Object from "./components/Object.vue";
import Array from "./components/Array.vue";

Vue.component("StringValue", StringValue);
Vue.component("Value", Value);
Vue.component("Value2", Value2);
Vue.component("Property", Property);
Vue.component("Object", Object);
Vue.component("Array", Array);

export default {
  name: "app",
  data: function() {
    return {
      value2Test: "B"
    }
  },
  computed: {

  },
  methods: {

  }
};
</script>

<style scoped>
#app {

}
</style>
