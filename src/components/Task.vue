<template>
  <div
    v-if="editing === true"
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      <input type="text" v-model="text" />
      <span>
        <Icon @confirm-edit="onConfirm(task.id)" type="confirm" :id="task.id" />
        <Icon
          @delete-task="$emit('delete-task', task.id)"
          type="delete"
          :id="task.id"
        />
      </span>
    </h3>
    <input type="text" v-model="day" />
  </div>

  <div
    v-else
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <span>
        <Icon @click="editTask" type="edit" :id="task.id" />
        <Icon
          @delete-task="$emit('delete-task', task.id)"
          type="delete"
          :id="task.id"
        />
      </span>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
import Icon from "./Icon";

export default {
  name: "Task",
  data() {
    return {
      editing: false,
      text: this.task.text,
      day: this.task.day,
      values: {},
    };
  },
  props: {
    task: Object,
  },
  components: {
    Icon,
  },
  methods: {
    editTask() {
      this.editing = !this.editing;
    },
    onConfirm(id) {
      this.values = {
        id,
        text: this.text,
        day: this.day,
      };
      this.$emit("confirm-edit", this.values);
      this.editing = false;
    },
  },
};
</script>

<style scoped>
.task {
  background: rgb(209, 202, 202);
  margin: 10px 0;
  padding: 10px;
  border-radius: 5px;
}

.task.reminder {
  border-left: 5px solid green;
}

h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

h3 i {
  cursor: pointer;
}
</style>