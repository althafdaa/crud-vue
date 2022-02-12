<template>
  <div class="flex gap-4 mb-2">
    <button
      class="text-gray-400"
      :class="{ 'font-bold': current === 'all' }"
      @click="updateFilter('all')"
    >
      SHOW ALL
    </button>
    <button
      class="text-gray-400"
      :class="{ 'font-bold': current === 'completed' }"
      @click="updateFilter('completed')"
    >
      FINISHED
    </button>
    <button
      class="text-gray-400"
      :class="{ 'font-bold': current === 'ongoing' }"
      @click="updateFilter('ongoing')"
    >
      ONGOING
    </button>
  </div>
</template>
<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(data) {
      this.$emit("filterChange", data);
    },
  },
};
</script>
<style></style>
