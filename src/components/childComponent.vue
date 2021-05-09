<template>
  <div>Child component</div>
  <!-- ***************************************** select ********************************************* -->

  <div id="v-model-select">
    <!-- 
    if we had "selected" in this component' scope we could have a 2-way binding as follows:
    <select v-model="selected">
      <option v-for="option in options" :value="option.value" v-bind:key="option.id">
        {{ option.text }}
      </option>
    </select> 
  -->
    <!-- BUT we get "selected" as props from the parent -->
    <!-- 
      Text and Textarea elements use the value property and the input event,
      Checkboxes and Radio buttons use the checked property and the change event 
      Select fields use the input property and the change event.
   -->
    <select
      :value="_selected"
      @change="$emit('update:_selected', $event.target.value)"
    >
      <option v-for="option in _options" :value="option.value" :key="option.id">
        {{ option.text }}
      </option>
    </select>

    <br />
  <!-- *************************************************************************************** -->



    <div >
      <label for="input-text">Text example:</label>
      <input
            type="text"
            id="input-text"
            :value="_text"
            @input="$emit('update:_text', $event.target.value)"
            />
    </div>




  <!-- ***************************************** checkbox ********************************************* -->
    <!-- 
      if we had only one bool value "_checked" passed as prop from the parent, we could follow the same implementation as input-text
      <input
      type="checkbox"
      :checked="_checked"
      @change="$emit('update:_checked', $event.target.checked)"
    /> -->

    <div>
      <div v-for="(elm, index) in _checkElms" :key="elm.id">
        <!-- The flwg line didn't work!, "emit('_change-checkbox" need to be fixed.
          <input type="checkbox" :id="elm.id" :value="elm.value" :checked="_checkedRes[index]" @change="$emit('update:_checkedRes',index , $event.target.checked)" /> 
          Instead we will emit a custom event as follows:
          -->
        <input type="checkbox" :id="elm.id" :value="elm.value" :checked="_checkedRes[index]" @change="$emit('_change-checkbox', index , $event.target.checked)" />
        <label :for="elm.id">{{ elm.viewValue }}</label>
      </div>
      <br />
      <!-- <span>Checked names: {{ checkedNames }}</span> -->
    </div>

  <!-- *************************************************************************************** -->
  </div>
</template>

<script>
export default {
  emits: ["_change-checkbox"],
  props: {

    _text:String,
    _options: {
      type: Array,
      required: true,
    },
    _selected: {
      type: String,
      default: "",
      required: true,
    },
    _checkElms: {
      type: Array,
      required: true,
    },
    _checkedRes: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
div {
  background-color: #97e8ee;
}
</style>
