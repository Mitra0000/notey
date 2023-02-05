<template>
  <li class="list-group-item">
    <div class="d-flex" style="align-items:baseline">
      <div class="no-grow time">{{ this.note.timestamp }}</div>
      <input 
          id="content" 
          ref="note-content" 
          :value="this.note.contents" 
          :disabled="!editing_mode" 
          v-on:keyup.enter="saveContents"
          v-on:blur="saveContents"
          autocomplete="off" >
      <div class="no-grow">
        <div class="btn-group-sm">
          <button class="btn" @click="editing_mode? saveContents() : editContents()">
            <i :class="['bi', editing_mode ? 'bi-check-lg' : 'bi-pencil']"></i>
          </button>
          <button class="btn" @click="$emit('delete-note', note.id)">
            <i class="bi bi-trash"></i>
          </button>
        </div>
      </div>
    </div>
  </li>
</template>

<script>

export default {
  name: 'NoteView',
  props: {
    note: Object,
  },
  data() {
    return {
      editing_mode: false,
    }
  },
  methods: {
    editContents() {
      this.editing_mode = true;
      this.$refs["note-content"].setAttribute("disabled", "false");
      this.$nextTick(() => this.$refs["note-content"].focus());
    },
    saveContents() {
      if (!this.editing_mode) return;
      this.editing_mode = false;
      this.$refs["note-content"].setAttribute("disabled", "true");
      this.$emit("update-note", this.note.id, this.$refs["note-content"].value);
    }
  }
}
</script>

<style scoped>
.time {
  border-right: 2px solid #4F4F4F;
  padding-right: 1rem;
}
#content {
  flex-grow: 1;
  padding-left: 1rem;
}
input {
  background-color: initial!important;
  color: initial;
  border-color: initial;
  border-style: initial;
}
</style>
  