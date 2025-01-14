<script setup>
    const props = defineProps({
        id: String,
        disabled: Boolean,
        value: String,
    })
    const model = defineModel()
</script>

<template>
  <label :for="id">
    <input
    :disabled="disabled"
      :id="id"
      type="radio"
      name="reponse"
      v-model="model"
      :value="value"
    />
    {{ value }}
  </label>
</template>
