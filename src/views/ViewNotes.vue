<template>
  <div class="notes">
    <div class="card has-background-success-dark p-4 mb-5">
      <div class="field">
        <div class="control">
          <textarea
            v-model="newNote"
            class="textarea"
            placeholder="Add a new note"
            ref="newNoteRef"
          />
        </div>
      </div>

      <div class="field is-grouped is-grouped-right">
        <div class="control">
          <button class="button is-link has-background-success" @click="addNewNote" :disabled="!newNote">
            Add New Note
          </button>
        </div>
      </div>
    </div>

    <Note
      v-for="note in notes"
      :key="note.id"
      :note="note"
    />
  </div>
</template>
<script setup>
import { ref } from 'vue';
import Note from '@/components/Notes/Note.vue';
const newNote = ref('')
const newNoteRef = ref(null)
const notes = ref([
  {
    id: 1,
    content: 'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quidem ipsa commodi sint ut ullam culpa nulla molestiae sunt quia qui maxime, enim quasi officiis aperiam fugit, corrupti omnis, eaque animi.',
  },
  {
    id: 2,
    content: 'shorter note',
  },
])

const addNewNote = () => {
  const currentDate = new Date().getTime()
  let note = {
    id: currentDate.toString(),
    content: newNote.value
  }

  notes.value.unshift(note)
  newNote.value = ''
  newNoteRef.value.focus()
}
</script>