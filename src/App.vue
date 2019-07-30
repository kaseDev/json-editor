<template>
  <div id="app">
    <!-- <Value v-model="valueTest" />
    <h1>{{valueTest}}</h1>
    <Value v-model="valueTest" /> -->
    <Property v-model="fieldTest" />
    <h1>{{fieldTest}}</h1>
    <Property v-model="fieldTest" />
    <button @click="printFieldTest">Print Object</button>
    <!-- <p>{{fieldTest}}</p> -->
    <!-- <Object v-model="objectTest2"/>
    <p>{{objectTest2}}</p>
    <Object v-model="objectTest2"/> -->

    <!-- <Value v-model="stringValueTest" /> -->
    <!-- <StringValue v-model="stringValueTest" /> -->
  </div>
</template>

<script>
import Vue from 'vue';
import StringValue from "./components/StringValue.vue";
import Value from "./components/Value.vue";
import Property from "./components/Property.vue";
import Object from "./components/Object.vue";


Vue.component("StringValue", StringValue);
Vue.component("Value", Value);
Vue.component("Property", Property);
Vue.component("Object", Object);

export default {
  name: "app",
  data: function() {
    return {
      valueTest: "this some text",
      fieldTest: {
        key: "name",
        value: null
      },
      objectTest: [
        {
          key: "name",
          value: "Jane Doe"
        },
        {
          key: "job",
          value: "CS student"
        },
        {
          key: "age",
          value: "20"
        }
      ],
      objectTest2: {
        name: "Jane Doe",
        job: "CS Student",
        age: "20"
      },
      stringValueTest: "Test Value"
    }
  },
  computed: {

  },
  methods: {
    printFieldTest: function() {
      console.log(this.fieldTest);
    }
  }
};
</script>

<style scoped>
#app {

}
</style>
