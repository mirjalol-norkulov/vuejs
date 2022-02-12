<template>
  <div class="container py-4">
    <table class="table">
      <thead>
        <tr>
          <th class="table-number-col">№</th>
          <th>Title</th>
          <th>Completed</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="todo.id">
          <td class="table-number-col">{{ index + start + 1 }}</td>
          <td>{{ todo.title }}</td>
          <td>
            <Icon size="18">
              <CheckOutlined v-if="todo.completed" />
              <CloseOutlined v-else />
            </Icon>
          </td>
          <td>
            <button class="btn btn-danger" @click="deleteTodo(todo.id)">
              <Icon size="18">
                <DeleteOutlined />
              </Icon>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <section class="row gx-1">
      <div class="col-auto">
        <button class="btn btn-primary" @click="handlePrevious">Oldingi</button>
      </div>
      <div class="col-auto">
        <button class="btn btn-primary" @click="handleNext">Keyingi</button>
      </div>
    </section>
    <LoadingOverlay v-show="isLoading" />
  </div>
</template>

<script>
import { Icon } from "@v2icons/utils";
import {
  CheckOutlined,
  CloseOutlined,
  DeleteOutlined,
} from "@v2icons/material";
import LoadingOverlay from "./LoadingOverlay.vue";
import { api } from "../api";

export default {
  components: {
    CheckOutlined,
    CloseOutlined,
    DeleteOutlined,
    Icon,
    LoadingOverlay,
  },
  data() {
    return {
      todos: [],
      limit: 10,
      start: 0,
      isLoading: false,
    };
  },
  watch: {
    start: {
      immediate: true,
      handler: "fetchTodos",
    },
  },
  methods: {
    async fetchTodos() {
      this.isLoading = true;
      const response = await api.get(
        `/todos?_limit=${this.limit}&_start=${this.start}`
      );
      this.todos = response.data;
      this.isLoading = false;
    },
    handlePrevious() {
      this.start = Math.max(this.start - this.limit, 0);
    },
    handleNext() {
      this.start += this.limit;
    },
    async deleteTodo(id) {
      this.isLoading = true;
      await api.delete(`/todos/${id}`);
      await this.fetchTodos();
      this.isLoading = false;
    },
  },
};
</script>

<style lang="scss">
.table-number-col {
  width: 70px;
}
</style>
