<template>
  <div v-if="!!sortField" class="zone-clickable" @click="onSortClick" :title="$t(title)">
    <span v-if="translateableLabel" v-t="translateableLabel"></span>
    <span v-else>{{ label }}</span>
    <nczone-sort-indicator v-if="sort.field === sortField" :order="sort.order" />
  </div>
  <div v-else :title="$t(title)">
    <span v-if="translateableLabel" v-t="translateableLabel"></span>
    <span v-else>{{ label }}</span>
  </div>
</template>
<script>
import { mapGetters, mapActions } from 'vuex'

export default {
  name: 'nczone-table-header-col',
  props: {
    sortField: {
      type: String,
      default: null
    },
    label: {
      type: String,
      default: null
    },
    title: {
      type: String,
      default: null
    }
  },
  computed: {
    translateableLabel () {
      return this.label && this.label !== '#' ? this.label : ''
    },
    ...mapGetters([
      'sort'
    ])
  },
  methods: {
    onSortClick () {
      this.setSort({ field: this.sortField })
    },
    ...mapActions([
      'setSort'
    ])
  }
}
</script>
