<template>
  <div class="h-screen bg-slate-200 flex items-center justify-center">
    <h1>Hello from world sayanaro</h1>
    <FormTask />
  </div>
</template>

<script>
import FormTask from "./components/FormTask.vue";

export default {
  name: "App",
  components: {
    FormTask,
  },
};
</script>
