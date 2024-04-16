<script>
import TableRowLayout from './TableRowLayout.vue'

export default {
  name: 'TableHeader',
  components: { TableRowLayout },
  methods: {
    sort () {
      this.$emit('sort')
    },
  },
}
</script>

<template>
  <table-row-layout>
    <template v-slot:name>
      <button @click="sort">Имя</button>
    </template>

    <template v-slot:phone>
      <span>Телефон</span>
    </template>
  </table-row-layout>
</template>
