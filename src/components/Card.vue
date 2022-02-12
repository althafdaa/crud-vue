<template>
  <div
    class="bg-white px-4 py-8 mb-4 rounded shadow-lg flex justify-between items-center border-l-4"
    :class="project.complete ? 'border-green-400' : 'border-red-400'"
  >
    <div>
      <h1 class="text-xl font-bold cursor-pointer" @click="showDetailHandler">
        {{ project.title }}
      </h1>
      <p class="mt-4" v-if="showDetails">{{ project.details }}</p>
    </div>
    <div class="flex gap-4">
      <span
        class="material-icons hover:text-red-500 cursor-pointer"
        @click="deleteHandler"
      >
        delete
      </span>
      <router-link :to="{ name: 'Edit', params: { id: project.id } }"
        ><span class="material-icons hover:text-blue-500 cursor-pointer">
          mode_edit
        </span></router-link
      >

      <span
        :class="project.complete ? 'text-green-600 font-bold' : ''"
        class="material-icons hover:text-green-500 cursor-pointer"
        @click="toggleDone"
      >
        done
      </span>
    </div>
  </div>
</template>
<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    showDetailHandler() {
      this.showDetails = !this.showDetails;
    },
    deleteHandler() {
      fetch(this.url, { method: "DELETE" }).then(() =>
        this.$emit("delete", this.project.id)
      );
    },
    toggleDone() {
      fetch(this.url, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ complete: !this.project.complete }),
      }).then(() => this.$emit("complete", this.project.id));
    },
  },
};
</script>
<style></style>
