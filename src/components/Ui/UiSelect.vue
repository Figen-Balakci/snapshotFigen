<script setup lang="ts">
defineProps<{ modelValue?: string | number; disabled?: boolean }>();

const emit = defineEmits(['update:modelValue', 'change']);

function handleChange(event) {
  emit('update:modelValue', event.target.value);
  emit('change', event.target.value);
}
</script>

<template>
  <TuneButton class="mb-2 flex w-full items-center overflow-hidden !px-3">
    <div class="no-shrink mr-2 text-skin-text">
      <slot name="label" />
    </div>
    <div v-if="$slots.image" class="no-shrink mr-2 text-skin-text">
      <slot name="image" />
    </div>
    <select
      :disabled="disabled"
      :value="modelValue"
      :class="{ disabled }"
      class="input h-full w-full flex-auto !bg-skin-bg"
      @change="handleChange($event)"
    >
      <slot />
    </select>
  </TuneButton>
</template>

<style scoped lang="scss">
.no-shrink {
  flex-shrink: 0;
}
.disabled {
  appearance: none;
}
</style>
