<template>
  <div class="container mx-auto">
    <h1 class="text-red-900">Hi there</h1>
    <div class="flex justify-center">
      <div class="mb-3 xl:w-96">
        <select
        v-model="current"
          class="form-select block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding bg-no-repeat border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          aria-label="Default select example"
        >
          <option selected>Page {{totalPage}}</option>
          <option v-for="page in totalPage" :key="page" :value="page">{{page}}</option>
        </select>
      </div>
    </div>
    <button @click="next" class="p-3 bg-blue-600 text-white">Next</button>
    <button @click="prev" class="p-3 bg-blue-600 text-white">Prev</button>
    <ul>
      <li v-for="(user, index) in paginated" :key="index">
        {{ user.id }} - {{ user.task }}
      </li>
    </ul>
  </div>
</template>

<script>
import partners from "../members/members.js";

export default {
  name: "Index",

  data() {
    return {
      users: partners,
      current: 1,
      pageSize: 50,
      total: partners.length,
    };
  },

  computed: {
    indexStart() {
      return (this.current - 1) * this.pageSize;
    },
    indexEnd() {
      return this.indexStart + this.pageSize;
    },
    paginated() {
      return this.users.slice(this.indexStart, this.indexEnd);
    },
    totalPage() {
      return this.total / this.pageSize;
    },
  },

  methods: {
    prev() {
      this.current--;
    },
    next() {
      this.current++;
    },
  },
};
</script>
