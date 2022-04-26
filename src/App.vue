<template>
  <div id="app">
    <div style="display: flex; justify-content: space-around; align-items: center">
      <div>
        <tools-autocomplect
          style="width: 200px"
          :datareturn="datareturn"
          :id="component_id"
          :css="css"
          :items="items">
        </tools-autocomplect>
      </div>
    <div>Result: {{ selected_value }}</div>
    </div>
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
      items: [
        {name: 'Peter', age: '20'},
        {name: 'Fader', age: '22'},
        {name: 'Sonya', age: '29'},
        {name: 'Sasha', age: '28'},
        {name: 'Anton', age: '28'},
        {name: 'Andrey', age: '18'},
        {name: 'Robert', age: '24'},
        {name: 'Rita', age: '25'},
        {name: 'James', age: '25'},
        {name: 'Moscow', age: '18'},
        {name: 'London', age: '24'},
        {name: 'Kiev', age: '25'},
        {name: 'Tokio', age: '25'},
      ],
      component_id: 'co1',
      css: [
        {"ac-wrapper": {"zIndex": 3, "height": "50px"}},
        {"ac-input": {"backgroundColor": "#f5f5f5", "fontSize": "115%"}},
        {"ac-button": {"color": "green" }},
        {"ac-items": {"backgroundColor": "#eee"}},
        {"ac-item": {"fontSize": "80%", "color": "#666"}},

      ],
      selected_value: '',
    }
  },
  methods: {
    datareturn(data) {
      this.selected_value = data;
    }
  }
}
</script>

<style>

</style>
