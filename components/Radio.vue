<template>
  <label :class="[theme.radio]">
    <span :class="radioClasses">
      <span :class="innerClasses"></span>
      <input type="radio" :checked="currentValue" @change="handleChange" :disabled="disabled || null" :name="name" :value="trueValue" />
    </span>
    <span class="radio-text"><slot></slot></span>
  </label>
</template>

<script type="text/javascript">
  import theme from './theme'
  export default {
    props: {
      value: {
        type: Boolean,
        default: false
      },
      disabled: {
        type: Boolean,
        default: false
      },
      name: {
        type: String,
        default: ''
      },
      trueValue: {
        type: [String, Number],
        default: ''
      }
    },
    computed: {
      radioClasses () {
        return [
          `sav-radio`,
          {
            [`sav-radio-checked`]: this.currentValue,
            [`sav-radio-disabled`]: this.disabled
          }
        ]
      },
      innerClasses () {
        return `sav-radio-inner`
      }
    },
    data () {
      return {
        theme,
        currentValue: this.value
      }
    },
    watch: {
      value () {
        this.updateModel()
      }
    },
    methods: {
      handleChange ($event) {
        if (this.disabled || $event.target.disabled) {
          $event.preventDefault()
          return
        }
  
        const checked = $event.target.checked
        this.currentValue = checked
        this.$emit('input', this.trueValue)
        this.$emit('change', this.trueValue)
      },
      updateModel () {
        this.currentValue = this.value
      }
    }
  }
</script>
