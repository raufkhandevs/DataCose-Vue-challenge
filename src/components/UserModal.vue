<template>
  <b-modal v-model="showModal" title="User Info" size="lg">
    <div v-if="user">
      <h5>Name: {{ user.name }}</h5>
      <p>Email: {{ user.email }}</p>
      <p>Phone: {{ user.phone }}</p>
      <p>Website: {{ user.website }}</p>
    </div>
  </b-modal>
</template>

<script>
export default {
  name: 'UserModal',
  props: {
    user: {
      type: Object,
      default: {},
    },
    showModal: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
