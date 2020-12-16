<template>
  <div :class="style.notesContent">
    <ol :class="style.containerNotes" v-if="list.length!==0">
      <li :class="style.notes" v-for="(note,index) in list" >
        <div>{{index+1}}</div>
        <div :class="style.textContent">{{note}}</div>
        <span :class="style.btn" @click="deleteNote(index)">Delete</span>
      </li>
    </ol>
    <h3 :class="style.noNotes" v-else>No notes</h3>
  </div>
</template>

<script>
  import style from "../../style/notes.module.scss"

  export default {
    data() {
      return {
        style: style,
      }
    },
    emits: ["delete-Note"],//не обязательно,но признак хорошего тона
    props: {list: Array},
    methods: {
      deleteNote(index) {
        //для изменения стэйта из другого компонента ,используется $emit("название события",параметр)
        this.$emit("delete-Note", index)
      },
    },
  }
</script>

