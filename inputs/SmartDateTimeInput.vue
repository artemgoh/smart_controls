<template>
  <input type="date" v-model="value" @input="typecast_value"/>
</template>
<script>
import moment from 'moment'

export default {
  name: 'SmartDateTimeInput',
  props: ['field', 'value'],
  methods: {
    typecast_value : function () {
      this.value = moment(this.value).format('YYYY-MM-DD')
    }
  }
}
</script>