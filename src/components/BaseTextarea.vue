<template>
  <div class="field message-field">
    <label :for="uuid" class="label">{{ label }}</label>
    <div class="control">
      <textarea
        :class="{'is-danger': error}"
        class="textarea is-primary"
        :placeholder="label"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :id="uuid"
      >
      </textarea>
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