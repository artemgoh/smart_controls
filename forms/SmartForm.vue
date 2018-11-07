<template>
  <form>
    <div v-for="row in rows" :key="row.id">
        <component
          :is="getComponentByType(field.type)"
          v-for="field in schema.fields"
          :key="field.name"
          :value="row[field.name]"
          :field="field"
        />
      </div>
    </div>
  </form>
</template>

<script>
import SmartInput from '../inputs/SmartInput'
import SmartChoiceInput from '../inputs/SmartChoiceInput'

export default {
  name: 'SmartForm',
  components: {
    SmartInput,
    SmartChoiceInput
  },
  props: {
    schema: {
      type: Object,
      required: true,
      validator(schema) {
        return 'fields' in schema && schema.fields instanceof Array
      }
    },
    dataSource: {
      type: Object,
      required: true,
      validator (dataSource) {
        return 'list' in dataSource && dataSource.list instanceof Function
      },
    }
  },
  data() {
    return {
      rows: []
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
        case 'foreign_key': {
          return 'SmartChoiceInput'
        }
        default : {
          return 'SmartInput'
        }
      }
    }
  }
}
</script>
