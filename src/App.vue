<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <child-component
    v-model:_selected="selectedOption"
    :_options="options"

    v-model:_text="textValue"
    
    :_checkElms="checkElms"
    :_checkedRes="checkedRes"
    @_change-checkbox="onChangeCheckbox"
  />

  <span>Selected: {{ selectedOption }}</span> <br />
  <span>Entered: {{ textValue }}</span> <br />
  <span>Checked: {{ checkedRes }}</span>
</template>

<script >
import { ref, reactive } from "vue";

import childComponent from "./components/childComponent.vue";

export default {
  components: {
    childComponent,
  },

  setup() {
    const selectedOption = ref("");
    const textValue = ref("");
    const checkedRes = reactive([false, false, false]);

    const options = [
      { id: 1, text: "One", value: "A" },
      { id: 2, text: "Two", value: "B" },
      { id: 3, text: "Three", value: "C" },
    ];
    const checkElms = [
      { id: 1, viewValue: "This is A1", value: "A1" },
      { id: 2, viewValue: "This is A2", value: "A2" },
      { id: 3, viewValue: "This is A3", value: "A3" },
    ];

    const onChangeCheckbox = (ind, val) => {
      console.log(`${ind} , ${val}`);

      // if(checkedRes[ind] != val){ //avoid loop?
      checkedRes[ind] = val;
      // }
      console.log(checkedRes);
    };

    return {
      selectedOption,
      options,
      textValue,
      checkElms,
      checkedRes,
      onChangeCheckbox,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
