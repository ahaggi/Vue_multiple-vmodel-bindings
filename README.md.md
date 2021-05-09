Using v-model on Components

The v-model directive now supports new defaults.

The default v-model property is renamed to modelValue instead of the old name of value.

The default v-model event is renamed to update:modelValue instead of the old name of input.

parent tamplet:
    <CustomComponent v-model:modelValue="name" />
<script >
export 