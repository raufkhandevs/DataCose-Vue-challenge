<template>
  <div>
    <b-table
      :items="items"
      :fields="fields"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      @row-clicked="showUser"
      striped
      bordered
      hover
    >
      <template #cell(title)="data">
        <b>{{ data.value }}</b>
      </template>
    </b-table>
  </div>
</template>

<script>
import UserModal from './UserModal.vue';

export default {
  components: { UserModal },
  props: {
    items: {
      type: Array,
      default: [],
    },
    fields: {
      type: Array,
      default: [],
    },
    sortBy: {
      type: Boolean,
      default: false,
    },
    sortDesc: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    showUser(todo) {
      this.$emit('showUser', todo);
    },
  },
};
</script>
