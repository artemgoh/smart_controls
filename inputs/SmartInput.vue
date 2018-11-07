<template>
  <div>
    <component
      :is="getComponentByType(field.type)"
      :field="field.name"
      v-model="value"
    ></component>
  </div>
</template>

<script>
import SmartStringInput from './SmartStringInput'
import SmartIntegerInput from './SmartIntegerInput'
import SmartDateTimeInput from './SmartDateTimeInput'

export default {
  name: 'SmartInput',
  components: {
    SmartStringInput,
    SmartIntegerInput,
    SmartDateTimeInput
  },
  props: ['value', 'field'],
  data() {
    return {
      rows: [],
    }
  },
  async beforeMount() {
    try {
      const data = await this.dataSource.list()

      this.rows = data
    } catch (e) {
      console.log('Failed to fetch data!')
    }
  },
  methods: {
    getComponentByType (field_type) {
      switch(field_type) {
        case 'string': {
          return 'SmartStringInput'
        }
        case 'date': {
          return 'SmartDateTimeInput'
        }
        case 'integer': {
          return 'SmartIntegerInput'
        }
        default : {
          return 'SmartStringInput'
        }
      }
    }
  }
}
</script>
