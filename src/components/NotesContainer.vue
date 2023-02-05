<template>
  <div class="mt-4 mb-4 h-100" style="flex-grow: 1; overflow-y: scroll;">
    <div class="card" style="height: 100%;">
      <ul id="logs" class="list-group">
        <NoteView v-for="note of this.notes" :key="note.id" :note="note" @update-note="updateNote" @delete-note="deleteNote"></NoteView>
      </ul>
    </div>
  </div>
</template>

<script>
import NoteView from "./NoteView.vue"

export default {
  name: 'NotesContainer',
  props: {
  },
  components: {
    NoteView,
  },
  data() {
    return {
      notes: [
      ],
    }
  },
  methods: {
    updateNote(id, newContents) {
      this.notes = this.notes.map((item) => item.id == id ? {...item, contents: newContents} : item);
    },
    deleteNote(id) {
      if (confirm("Are you sure you want to delete this note?")) {
        this.notes = this.notes.filter((item) => item.id != id);
      }
    },
    addNote(time, newContents) {
      this.notes = [...this.notes, {id: this.notes.length, timestamp: time, contents: newContents}];
    },
    copyToClipboard() {
      navigator.clipboard.writeText(this.getNotes());
    },
    downloadNotes() {
      let element = document.createElement('a');
      element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(this.getNotes()));
      element.setAttribute('download', "notes.txt");

      element.style.display = 'none';
      document.body.appendChild(element);

      element.click();

      document.body.removeChild(element);
    },
    getNotes() {
      return this.notes.map((item) => item.timestamp + ": " + item.contents).join("\n");
    },
  }
}
</script>

<style scoped>
li:nth-child(odd) {
  background: #F4FAFF;
}
</style>
