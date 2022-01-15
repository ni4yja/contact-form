<template>
  <div class="field">
    <label :for="uuid" class="label">{{ label }}</label>
    <div class="control">
      <input
        v-bind="$attrs"
        :placeholder="label"
        class="input is-primary"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :id="uuid"
        :aria-describedby="error ? `${uuid}-error` : null"
        :aria-invalid="error ? true : null"
      />
      <p
        v-if="error"
        class="help is-danger"
        :id="`${uuid}-error`"
        aria-live="assertive"
      >
       {{ error }}
      </p>
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
    },
    error: {
      type: String,
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

<style>

</style>