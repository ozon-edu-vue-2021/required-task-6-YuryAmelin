<template>
  <div id="app">
    <oz-table :rows="rows">
      <oz-table-column prop="id" title="ID" />
      <oz-table-column prop="postId" title="Post ID" />

      <oz-table-column prop="email">
        <template #title>
          <b>Email</b>
        </template>

        <template #body="{ row }">
          <a :href="`mailto:${row.email}`">{{ row.email }}</a>
        </template>
      </oz-table-column>

      <oz-table-column prop="name" title="Name" />
    </oz-table>
  </div>
</template>

<script>
import OzTable from '@/components/oz-table';
import OzTableColumn from '@/components/oz-table-column';

export default {
  name: 'App',
  components: {
    OzTableColumn,
    OzTable
  },
  async created() {
    const res = await fetch('https://jsonplaceholder.typicode.com/comments')
    this.rows = await res.json()
  },
  data() {
    return {
      rows: []
    };
  }
};
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
