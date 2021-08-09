<template>
  <v-container style="max-width: 1185px">
    <h1 class="text-center mb-5">Note App</h1>
    <h4 class="text-center my-10">Add Your Notes</h4>

    <div class="align-center">
      <v-text-field
        label="Add Notes"
        v-model="mynote"
        solo
        class="mx-5"
      ></v-text-field>
      <v-btn
        v-on:click="addNotes"
        class="d-flex ma-auto"
        fab
        dark
        large
        color="green"
      >
        <v-icon darks> mdi-plus </v-icon>
      </v-btn>
    </div>

    <table class="text-center" width="1000">
      <tr>
        <th class="ma-5">Description</th>
        <th class="ma-5">Edit</th>
        <th class="pa-5">Delete</th>
      </tr>
      <tr v-for="(note, index) in notes" :key="index">
        <!-- <td>{{ note.id }}</td> -->
        <td>{{ note.desc }}</td>
        <td>
          <v-icon @click="editNote(index)" color="green"> mdi-pencil </v-icon>
        </td>
        <td>
          <v-icon v-on:click="deleteNote(index)" darks color="red">
            mdi-delete
          </v-icon>
        </td>
      </tr>
    </table>
  </v-container>
</template>

<script lang="ts">
export default {
  name: "Notes",
  data() {
    return {
      notes: [
        {
          desc: "This is The First Note",
        },
      ],
      mynote: "",
      editedNote: null,
    };
  },
  methods: {
    addNotes() {
      if (this.mynote.length) {
        if (this.editedNote === null) {
          console.log(this.mynote);
          this.notes.push({
            desc: this.mynote,
          });
        } else {
          this.notes[this.editedNote].desc = this.mynote;
          this.editedNote = null;
        }
        this.mynote = "";
      } else {
        alert("Text Field cannot be empty");
      }
    },
    deleteNote(index) {
      this.notes.splice(index, 1);
    },
    editNote(index) {
      this.mynote = this.notes[index].desc;
      this.editedNote = index;
    },
  },
};
</script>