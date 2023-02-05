<template>
  <div class="input-group fixed-bottom p-2">
    <input 
        ref="text-input" 
        class="form-control" 
        v-model="this.newNote"
        v-on:keyup.enter="submitNote"
        autofocus 
        autocomplete="off" />
    <button class="btn input-gropup-addon" @click="submitNote()">
      <i class="bi bi-chat-left-text"/>
    </button>
  </div>
</template>

<script>

export default {
  name: 'AddNote',
  data() {
    return {
      newNote: "",
    }
  },
  methods: {
    submitNote() {
      this.$emit('add-note', this.newNote);
      this.newNote = "";
      this.$refs["text-input"].focus();
    }
  }
}
</script>

<style>
</style>
