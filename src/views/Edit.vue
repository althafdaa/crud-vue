<template lang="">
  <form @submit.prevent="submitHandler" class="flex flex-col">
    <div class="flex flex-col mb-4">
      <label class="text-xl font-bold mb-2" for="title">Title</label>
      <input
        class="p-4"
        type="text"
        placeholder="Enter your project title"
        v-model="title"
      />
    </div>
    <div class="flex flex-col">
      <label class="text-xl font-bold mb-2" for="fill">Details</label>
      <textarea
        rows="8"
        class="p-4"
        placeholder="Details of the projects"
        v-model="details"
      />
    </div>
    <button
      class="font-bold py-2 px-4 self-end bg-green-600 my-2 text-white rounded-lg shadow-lg hover:bg-green-700"
    >
      Edit Project
    </button>
  </form>
</template>
<script>
import router from "../router";

export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
    };
  },
  mounted(id) {
    fetch(`http://localhost:3000/projects/${this.id}`)
      .then((x) => x.json())
      .then((y) => {
        this.title = y.title;
        this.details = y.details;
      });
  },
  methods: {
    submitHandler() {
      let project = {
        title: this.title,
        details: this.details,
      };
      fetch(`http://localhost:3000/projects/${this.id}`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(project),
      }).then(() => router.push("/"));
      this.title = "";
      this.details = "";
    },
  },
};
</script>
<style lang=""></style>
