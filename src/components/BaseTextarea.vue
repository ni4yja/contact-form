<template>
  <div class="field message-field">
    <label :for="uuid" class="label">{{ label }}</label>
    <div class="control">
      <textarea
        class="textarea is-primary"
        :placeholder="label"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :id="uuid"
      ></textarea>
    </div>
  </div>
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