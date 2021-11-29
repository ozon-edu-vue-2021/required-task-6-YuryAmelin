<template>
  <div class="wrapper">
    <button @click="switchMode">Поменять режим пагинации</button>
    <oz-table
      :rows="rows"
      :total-pages="100"
      :current-page="currentPage"
      :static-paging="staticPaging"

      @getPage="getPage"
    >
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
import OzTable from './oz-table';
import OzTableColumn from './oz-table-column';

export default {
  name: 'PagingWrapper',
  components: {
    OzTableColumn,
    OzTable
  },
  created() {
    this.blockingPromise = this.getPage(1);
  },
  data() {
    return {
      rows: [],
      currentPage: 1,
      staticPaging: true,
    };
  },
  methods: {
    async switchMode() {
      this.rows = []
      this.currentPage = 1
      if (this.staticPaging) {
        await this.getPage(1)
        this.staticPaging = !this.staticPaging
      } else {
        this.staticPaging = !this.staticPaging
        await this.getPage(1)
      }
    },
    async getPage(number) {
      if (this.staticPaging) {
        const res = await fetch(`https://jsonplaceholder.typicode.com/comments?postId=${number}`);
        this.rows = await res.json();
        this.currentPage = number;
      } else {
        this.blockingPromise && await this.blockingPromise;
        const res = await fetch(`https://jsonplaceholder.typicode.com/comments?postId=${this.currentPage + 1}`);
        const newRows = await res.json();
        const res2 = await fetch(`https://jsonplaceholder.typicode.com/comments?postId=${this.currentPage + 2}`);
        const newRows2 = await res2.json();
        this.rows = [...this.rows, ...newRows, ...newRows2];
        this.currentPage++;
      }
    },
  }
};
</script>
