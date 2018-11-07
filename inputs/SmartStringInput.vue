<template>
    <input type="text" :value="value"/>
</template>
<script>
export default {
  name: 'SmartStringInput',
  props: ['field', 'value']
}
</script>