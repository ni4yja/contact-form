<template>
  <div class="field">
    <label class="label">{{ label }}</label>
    <div class="control">
      <component
        v-for="option in options"
        :key="option.value"
        :is="vertical ? 'div' : 'span'"
        :class="{
          horizontal: !vertical
        }"
      >
        <BaseRadio
          :label="option.label"
          :value="option.value"
          :name="name"
          :modelValue="modelValue"
          @update:modelValue="$emit('update:modelValue', $event)"
        />
      </component>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    options: {
      type: Array,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    modelValue: {
      type: [String, Number],
      required: true,
    },
    vertical: {
      type: Boolean,
      default: false
    }
  },
};
</script>

<style scoped> 
.horizontal {
  margin-right: 20px;
}
</style>