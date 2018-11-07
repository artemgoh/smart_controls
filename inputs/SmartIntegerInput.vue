<template>
  <input type="number" v-model="value" @input="typecast_value"/>
</template>
<script>
export default {
  name: 'SmartIntegerInput',
  props: ['field', 'value'],
  methods: {
    typecast_value : function () {
      this.value = parseInt(this.value)
    }
  }
}
</script>