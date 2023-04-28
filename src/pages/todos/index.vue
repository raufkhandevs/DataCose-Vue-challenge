<template>
  <div>
    <h1 class="mb-4">Posts List</h1>

    <b-form-group label="Search by title">
      <b-form-input v-model="search" debounce="500"></b-form-input>
    </b-form-group>

    <Table
      @showUser="showUserModalData"
      :items="filteredTodos"
      :fields="fields"
    />

    <user-modal :showModal="showUserModal" :user="user" />
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      todos: [],
      search: '',
      perPage: 10,
      currentPage: 1,
      sortBy: 'id',
      sortDesc: false,
      showUserModal: false,
      user: null,
      fields: [
        { key: 'title', label: 'Title' },
        { key: 'completed', label: 'Completed' },
      ],
    };
  },
  async created() {
    const { data } = await axios.get(
      'https://jsonplaceholder.typicode.com/todos'
    );
    this.todos = data;
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) =>
        todo.title.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  methods: {
    async showUserModalData(todo) {
      const { data } = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${todo.userId}`
      );
      this.user = data;
      this.showUserModal = true;
    },
  },
};
</script>
