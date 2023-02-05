<template>
  <div class="container">
    <HeaderComponent></HeaderComponent>
    <TimerComponent ref="timer-component" @copy-to-clipboard="copyNotes()" @download-notes="downloadNotes()"></TimerComponent>
    <NotesContainer ref="notes-container"></NotesContainer>
    <AddNote @add-note="createNote"></AddNote>
  </div>
</template>

<script>
import AddNote from "./components/AddNote.vue"
import HeaderComponent from "./components/HeaderComponent.vue"
import NotesContainer from "./components/NotesContainer.vue"
import TimerComponent from "./components/TimerComponent.vue"

export default {
  name: 'App',
  components: {
    AddNote,
    HeaderComponent,
    NotesContainer,
    TimerComponent,
  },
  methods: {
    createNote(contents) {
      if (contents.trim() == "") {
        return;
      }
      this.$refs["notes-container"].addNote(this.$refs["timer-component"].getTime(), this.sanitise(contents));
      this.$refs["timer-component"].startTimer();
    },
    copyNotes() {
      this.$refs["notes-container"].copyToClipboard();
    },
    downloadNotes() {
      this.$refs["notes-container"].downloadNotes();
    },
    sanitise(text) {
      let words = text.split(" ");
      // TODO: Find a way to distinguish between her (possessive) and her (referential).
      for (let i = 0; i < words.length; i++) {
        let word = words[i].toLowerCase();
        if (word == "he" || word == "him" || word == "she" || word == "her" || word == "they") {
          words[i] = "TC";
        } else if (word == "his" || word == "their") {
          words[i] = "TC's";
        }
      }
      return words.join(" ");
    },
  }
}
</script>

<style>
.no-grow {
  flex-grow: 0;
}
</style>
