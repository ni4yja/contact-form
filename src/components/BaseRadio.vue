<template>
  <label :for="uuid" v-if="label" class="radio">
    <input 
      type="radio"
      :checked="modelValue === value"
      :value="value"
      v-bind="$attrs"
      @change="$emit('update:modelValue', value)"
     :id="uuid"
    >
    {{ label }}
  </label>
</template>

<script>
import UniqueID from "../features/UniqueID"

export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    },
    value: {
      type: [String, Number],
      required: true
    }
  },
  setup () {
    const uuid = UniqueID().getID()
    return {
      uuid
    }
  }
}
</script>

<style>

</style>