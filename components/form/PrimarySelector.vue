<template>
  <div>
    <label v-if="label" class="block text-gray-700 dark:text-slate-300 text-sm font-bold font-['Nunito'] mb-2"
           :for="id">
      {{ label }}
    </label>
    <select
      class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline
             focus:ring transition duration-300
             dark:bg-slate-800 dark:text-slate-300 dark:border-slate-600"
      :class="{'text-gray-300 dark:text-slate-500 bg-gray-50': disable}"
      :id="id" :value="value" @input="$emit('input', $event.target.value)" :disabled="disable">
      <option v-for="(option, k) in options" :k="k" :value="option.value">{{
          (option.label === $t(option.label)) ? option.label : $t(option.label)
        }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "PrimarySelector",
  props: {
    id: {
      type: String,
      default: 'primary-select',
    },
    label: {
      type: String,
      default: null,
    },
    value: {
      type: [String, Number],
      default: '',
    },
    disable: {
      type: Boolean,
      default: false,
    },
    options: {
      type: Array,
      default: () => [
        {
          value: '',
          label: '请选择',
        },
      ],
    },
  },
  methods: {}
}
</script>

<style scoped>

</style>
