<template>
  <div class="form-todo form-group">
    <p>
      <input
        type="text"
        placeholder="nome"
        name="author"
        class="form-control"
        v-model="name"
      />
    </p>

    <p>
      <textarea
        placeholder="Comentário"
        name="message"
        class="form-control"
        v-model="message"
      ></textarea>
    </p>

    <button
      v-on:click.prevent="addComment"
      type="submit"
      class="btn btn-primary"
    >
      Comentar
    </button>
  </div>
</template>

<script>
export default {
  name: "FormTodo",
  data() {
    return {
      name: "",
      message: "",
      id: 1
    };
  },
  methods: {
    addComment() {
      if (!this.message.trim()) {
        return;
      }

      this.$emit("add-todo", {
        name: this.name,
        message: this.message,
        id: this.getId()
      });

      this.name = "";
      this.message = "";
    },
    getId() {
      return this.id++;
    }
  }
};
</script>
