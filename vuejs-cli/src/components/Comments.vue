<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <FormTodo v-on:add-todo="addComment" />

    <div class="list-group">
      <p v-if="comments.length <= 0">Sem comentários...</p>

      <div
        v-else
        class="list-group-item"
        v-bind:key="comment.id"
        v-for="(comment, index) in allComments"
      >
        <span class="comment__author">
          Author: <strong>{{ comment.name }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">
            Excluir
          </a>
        </div>
      </div>
    </div>

    <hr />
  </div>
</template>

<script>
import FormTodo from "./FormTodo";

export default {
  name: "Comments",
  components: {
    FormTodo
  },
  data() {
    return {
      comments: []
    };
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(index) {
      this.comments.splice(index, 1);
    }
  },
  computed: {
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() ? comment.name : "Anônimo"
      }));
    }
  },
  watch: {
    comments(comments) {
      console.log("watch - listener of comments", comments);
    }
  }
};
</script>
