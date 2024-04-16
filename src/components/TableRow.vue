<script>
import TableRowLayout from './TableRowLayout.vue'

export default {
  name: 'TableRow',
  components: { TableRowLayout },
  props: {
    user: Object,
    depth: Number,
  },
  data () {
    return {
      isChildrenVisible: true,
      DEPTH_LIMIT: 4,
    }
  },
  methods: {
    toggleChildrenVisibility () {
      this.isChildrenVisible = !this.isChildrenVisible
    },
    sort (id) {
      this.$emit('sort', id)
    },
  },
  computed: {
    hasChildren () {
      return !!this.user.children.length
    },
  },
}
</script>

<template>
  <table-row-layout>
    <template v-slot:name>
      <button v-if="hasChildren" @click="toggleChildrenVisibility">
        <img v-if="isChildrenVisible" src="../assets/icons/minus.svg">

        <img v-else src="../assets/icons/plus.svg">
      </button>

      <span>{{ user.name }}</span>
    </template>

    <template v-slot:phone>
      <span>{{ user.phone }}</span>
    </template>

    <template v-slot:children>
      <ul v-if="hasChildren && isChildrenVisible" :class="{'row__list--wo-left-padding': depth > DEPTH_LIMIT}">
        <table-row v-for="user in user.children" :key="user.id" :user="user" :depth="depth + 1" />
      </ul>
    </template>
  </table-row-layout>
</template>

<style>
.row__list--wo-left-padding li {
  padding-left: 0;
}
</style>
