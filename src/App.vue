<template>
  <div id="app">
    <tools-autocomplect style="width: 200px" :id="com_id" :css="css" :items="d"></tools-autocomplect>
  </div>
</template>

<script>

import toolsAutocomplect from "@/components/toolsAutocomplect";

export default {
  name: 'App',
  components: {
    toolsAutocomplect
  },
  data() {
    return {
      d: [
        {name: 'Peter', age: '20'},
        {name: 'Fader', age: '22'},
        {name: 'Sonya', age: '29'},
        {name: 'Sasha', age: '28'},
        {name: 'Anton', age: '28'},
        {name: 'Andrey', age: '18'},
        {name: 'Robert', age: '24'},
        {name: 'Rita', age: '25'},
      ],
      com_id: 'co1',
      css2: [],
      css: [
        {"ac-wrapper": {"zIndex": 3, "height": "50px"}},
        {"ac-input": {"backgroundColor": "#eee", "fontSize": "115%"}},
        {"ac-items": {"backgroundColor": "#ccc"}},
        {"ac-item": {"fontSize": "80%", "color": "green"}},
        {"hovers": {"backgroundColor": "#ddd"}},
      ]
    }
  },
}
</script>

<style>

</style>
