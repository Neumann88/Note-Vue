<template>
  <div :class="style.main">
    <h1 :class="style.title">Enter your notes</h1>
    <input
      :class="style.input"
      type="text"
      @keydown.enter="createNote"
      v-model="inputValue"
      placeholder="Enter your note"
    />
    <Notes v-bind:list="notesValue" @delete-Note="deleteNote" />
  </div>
</template>

<script>
import style from "../style/notesMain.module.scss";
import Notes from "./notesComponents/notes.vue";

export default {
  //пропсы,если передавать как объект то в значении указывать typeof
  props: {},
  //компоненты
  components: { Notes },

  data() {
    return {
      //для модулей css добавляем импорт в стэйт(не знаю правильно ли так делать или нет,но работает)
      style: style,
      inputValue: "",
      //массив куда пушим содержимое инпута
      notesValue: [],
    };
  },
  //хук жиз цикл (Обычно его используют для извлечения данных для компонента и изменения DOM)
  mounted() {
    if (localStorage.getItem("notesValue")) {
      try {
        this.notesValue = JSON.parse(localStorage.getItem("notesValue"));
      } catch (e) {
        localStorage.removeItem("notesValue");
      }
    }
  },
  methods: {
    createNote() {
      if (!this.inputValue) {
        return;
      }
      //взяли массив и запушили туда значение из инпута
      this.notesValue.push(this.inputValue);
      //получаем прокси
      //console.log(this.notesValue);
      //обнуляем инпут
      this.inputValue = "";
      this.saveNotes();
    },
    deleteNote(index) {
      this.notesValue.splice(index, 1);
      this.saveNotes();
    },
    saveNotes() {
      const parsed = JSON.stringify(this.notesValue);
      localStorage.setItem("notesValue", parsed);
    },
  },
};
</script>
