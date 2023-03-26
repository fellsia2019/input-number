<template>
  <input
    type="text"
    @input="onInput"
    @beforeinput="onBeforeinput"
    @keydown="onKeydown"
  >
</template>

<script>
export default {
  data() {
    return {
      reg: /[^0-9\.]/g
    }
  },
  methods: {
    testValueFormInput(e, handler) {
      const expectedValue = e.data ? e.target.value + e.data : e.target.value

      if (
        expectedValue.match(this.reg)
        || expectedValue.startsWith('.')
        || ((e.target.value && e.target.value.indexOf('.') !== -1) && (e.data && e.data.indexOf('.') !== -1))
      ) {
        handler()
      }
    },
    onBeforeinput(e) {
      this.testValueFormInput(e, ()=> { e.preventDefault() })
    },
    onKeydown(e) {
      const isValidKeys = ['1','2','3','4','5','6','7','8','9','0','.']
      const expectedValue = e.target.value + e.key

      if (
        !isValidKeys.includes(e.key)
        || expectedValue.startsWith('.')
        || (e.target.value.indexOf('.') !== -1 && e.key == '.')
      ) {
        e.preventDefault()
      }
    },
    onInput(e) {
      this.testValueFormInput(e, ()=> {
        e.target.value = e.target.value.replace(this.reg, '')
      })
    }
  }
}
</script>