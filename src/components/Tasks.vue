<template>
  <div>
    <div :key="task.id" v-for="task in tasks">
      <Task
        @toggle-reminder="$emit('toggle-reminder', task.id)"
        @delete-task="$emit('delete-task', task.id)"
        @confirm-edit="onConfirm"
        :task="task"
      />
    </div>
  </div>
</template>

<script>
import Task from "./Task";
export default {
  name: "Tasks",
  data() {
    return {
      values: {},
    };
  },
  props: {
    tasks: Array,
  },
  components: {
    Task,
  },
  methods: {
    onConfirm(values) {
      this.$emit("confirm-edit", values);
    },
  },
};
</script>