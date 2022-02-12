<template>
  <Filter @filterChange="current = $event" :current="current" />
  <div v-if="projects.length">
    <div v-for="project in filteredProjects" :key="project.id">
      <Card
        :project="project"
        @delete="deleteLocalHandler"
        @complete="doneLocalHandler"
        @add="addLocalHandler"
      />
    </div>
  </div>
</template>

<script>
import Card from "../components/Card.vue";
import Filter from "../components/Filter.vue";
export default {
  name: "Home",
  components: { Card, Filter },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },

  mounted() {
    fetch("http://localhost:3000/projects")
      .then((x) => x.json())
      .then((data) => (this.projects = data));
  },
  methods: {
    deleteLocalHandler(id) {
      this.projects = this.projects.filter((e) => e.id !== id);
    },
    doneLocalHandler(id) {
      let p = this.projects.find((e) => e.id === id);
      p.complete = !p.complete;
    },
    addLocalHandler(data) {
      this.projects.push(data);
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === "completed")
        return this.projects.filter((e) => e.complete);
      if (this.current === "ongoing")
        return this.projects.filter((e) => !e.complete);
      else return this.projects;
    },
  },
};
</script>
