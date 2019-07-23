<template>
  <div id="app">
    <!-- <Value v-model="valueTest" />
    <h1>{{valueTest}}</h1>
    <Value v-model="valueTest" /> -->
    <!-- <Property v-model="fieldTest"/>
    <h1>{{fieldTest}}</h1>
    <Property v-model="fieldTest" /> -->

    <!-- <p>{{fieldTest}}</p> -->
    <Object v-model="objectTest2"/>
    <p>{{objectTest2}}</p>
    <Object v-model="objectTest2"/>
  </div>
</template>

<script>
import Value from "./components/Value.vue";
import Property from "./components/Property.vue";
import Object from "./components/Object.vue";

export default {
  name: "app",
  components: {
    Value,
    Property,
    Object
  },
  data: function() {
    return {
      valueTest: "this some text",
      fieldTest: {
        key: "this is the key",
        value: "This is the value"
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
      }
    }
  },
  computed: {

  },
  methods: {

  }
};
</script>

<style>
#app {

}
</style>
