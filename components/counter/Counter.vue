<script lang="ts" setup>
const localCounter = ref<number>(0)
const doubledLocalCounter = computed<number>(() => localCounter.value * 2)

const globalCounter = useGlobalCounterComposable()

const props = defineProps<{
  counterId: string,
  propCount:  globalThis.Ref<number>,
  propDoubledCount:  globalThis.ComputedRef<number>,
}>()

const emits = defineEmits(['emitIncrement'])

</script>

<template>
  <fieldset>
    <legend>Counter {{ counterId }}</legend>

    <button @click.prevent="localCounter++" class="me-1">
      Local: {{ localCounter }} * 2 = {{ doubledLocalCounter }}
    </button>

    <button @click.prevent="globalCounter.increment" class="me-1">
      Global: {{ globalCounter.count }} * 2 = {{ globalCounter.doubledCount }}
    </button>

    <button @click.prevent="emits('emitIncrement')">
      Parent: {{ props.propCount }} * 2 = {{ props.propDoubledCount }}
    </button>

  </fieldset>
</template>

<style scoped>
button.me-1 {
  margin-right: 1rem;
}
</style>