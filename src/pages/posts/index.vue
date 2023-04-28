<template>
  <div>
    <h1 class="mb-4">Posts List</h1>

    <b-form-group label="Search by title">
      <b-form-input v-model="searchText" debounce="500"></b-form-input>
    </b-form-group>

    <Table @showUser="showUserModal" :items="filteredTodos" :fields="fields" />

    <user-modal :showModal="showModal" :user="user" />
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      todos: [],
      searchText: '',
      sortBy: 'title',
      sortDesc: false,
      showModal: false,
      user: null,
      fields: [
        { key: 'title', label: 'Title' },
        { key: 'body', label: 'Body' },
      ],
    };
  },

  computed: {
    filteredTodos() {
      return this.todos.filter((todo) =>
        todo.title.toLowerCase().includes(this.searchText.toLowerCase())
      );
    },
  },

  async mounted() {
    const response = await axios.get(
      'https://jsonplaceholder.typicode.com/posts'
    );
    this.todos = response.data;
  },

  methods: {
    async showUserModal(todo) {
      const response = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${todo.userId}`
      );
      this.user = response.data;
      this.showModal = true;
    },
  },
};
</script>
