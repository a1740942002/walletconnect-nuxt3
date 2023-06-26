<template>
  <RadioGroup
    v-model="model"
    class="tw-inline-flex tw-bg-dim-1 tw-p-3 tw-rounded tw-gap-2"
  >
    <RadioGroupOption
      v-for="(option, index) of options"
      :key="getKey(option, index)"
      v-slot="{ checked }"
      :value="getValue(option)"
    >
      <slot name="option" v-bind="{ option, checked }">
        <div class="tw-radio-option tw-clickable" :class="{ checked }">
          <RadioGroupLabel as="div" class="tw-z-1">
            <span class="tw-font-medium">
              {{ option }}
            </span>
          </RadioGroupLabel>
        </div>
      </slot>
    </RadioGroupOption>
  </RadioGroup>
</template>

<script setup lang="ts">
import { RadioGroup, RadioGroupLabel, RadioGroupOption } from '@headlessui/vue'
import { useVModel } from '@vueuse/core'

type Value = any
type Option = any

interface Props {
  modelValue: Value
  options?: Option[]

  // How to render list of the options
  getKey?: (_option: Option, _index: number) => string | number

  // Getter to a value to use as a model
  getValue?: (_option: Option) => Value
}

const props = withDefaults(defineProps<Props>(), {
  options: () => [],
  getKey: (_option: Option, index: number) => index,
  getValue: (option: Option) => option
})

const model = useVModel(props)
</script>
