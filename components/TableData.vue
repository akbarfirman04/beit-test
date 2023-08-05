<template>
  <div>
    <v-data-table
      :headers="header"
      :items="data"
      :items-per-page="5"
      class="elevation-1"
    ></v-data-table>
  </div>
</template>
<script>
export default {
  props: {
    data: {
      type: Array,
      default: null,
    },
    header: {
      type: Array,
      default: null,
    },
  },
  setup() {},
}
</script>
