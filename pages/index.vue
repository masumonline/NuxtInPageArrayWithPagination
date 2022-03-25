<template>
  <div class="container mx-auto">
    <h1 class="text-red-900">Hi there</h1>
    <input type="number" v-model="current" />
    <button @click="next" class="p-3 bg-blue-600 text-white">Next</button>
    <button @click="prev" class="p-3 bg-blue-600 text-white">Prev</button>
    <ul>
      <li v-for="(user, index) in paginated" :key="index">
        {{index}} - {{ user.id }} - {{ user.task }}
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
      pageSize: 10,
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
