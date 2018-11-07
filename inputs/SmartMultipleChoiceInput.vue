<template>
  <div>
    <select v-model="value" multiple>
        <option v-for="(value, key) in field.choices" :key=key :value=key>{{ value }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'SmartInput',
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
  }
}
</script>
