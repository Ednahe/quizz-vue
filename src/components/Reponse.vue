<script setup>
import { computed } from "vue";

const props = defineProps({
  id: String,
  disabled: Boolean,
  value: String,
  correctReponse: String,
});
const model = defineModel();
const emits = defineEmits(['change'])
const onChange = (event) => {
  emits('change', event)
}
const classes = computed(() => ({
  disabled: props.disabled,
  right: props.disabled && props.value === props.correctReponse,
  wrong: props.disabled && props.value !== props.correctReponse && model.value === props.value,
}));
</script>

<template>
  <label :for="id" :class="classes">
    <input
      :disabled="disabled"
      :id="id"
      type="radio"
      name="reponse"
      v-model="model"
      :value="value"
      @change="onChange"
    />
    {{ value }}
  </label>
</template>

<style>
.right {
  color: green;
  opacity: 1;
}
.wrong {
  color: red;
  opacity: 1;
}
.disabled {
  opacity: 0.5;
}
</style>
