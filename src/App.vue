<script>
  export default {
      data(){
        return{
          noteText: '',
          noteDeadline: '',
          notes: JSON.parse(localStorage.getItem('notes')),


        }
      },
    methods:{
      createNote(){
        this.notes.push({
          text: this.noteText,
          deadline: this.noteDeadline,
        })
        localStorage.setItem('notes', JSON.stringify(this.notes));
        console.log()
      },
      deleteNote(index){
        this.notes.splice(index, 1)
      }
    }
  }

</script>

<template>
<div class="workspace">
  <div class="creation-space">
    <div class="inputs">
      <div class="input-cont" style="flex-grow: 2">
      <span class="label">
        Заметка
      </span>
        <textarea placeholder="Заметка" v-model="noteText"></textarea>
      </div>
      <div class="input-cont">
      <span class="label">
        Дата завершения
      </span>
        <input type="text" placeholder="Дата" v-model="noteDeadline">
      </div>
    </div>
    <button class="new-note" @click="createNote">Создать заметку</button>
  </div>
  <div class="notes-space">
    <div class="note" v-for="(note, index) in notes">
      <div class="text">{{note.text}}</div>
      <div class="deadline">{{note.deadline}}</div>
      <button class="delete-note" @click="deleteNote(index)">Удалить</button>
    </div>
  </div>
</div>

</template>

<style scoped>
*{
  box-sizing: border-box;
  font-size: 24px;
  font-family: Calibri;
}
.workspace{
  width: 700px;
  min-height: 700px;
  background: #ffffff;
  margin: 0 auto;
  border-radius: 5%;
  box-shadow: 10px 10px 30px;
  padding: 20px;
}
.creation-space{
  padding-bottom: 40px;
  border-bottom: 3px solid rgba(0, 0, 0, 0.14);
}
.inputs{
  display: flex;
  width: 100%;
  gap: 20px;
  margin-bottom: 20px;
}

.input-cont span{
  display: block;
  margin-bottom: 10px;
  font-weight: 700;
}

.input-cont input, textarea{
  padding: 10px;
  border-radius: 15px;
  resize: none;
  border: 1px solid rgba(0, 0, 0, 0.14);
  outline: none;
  width: 100%;
}

.input-cont textarea{
  height: 150px;
}

.input-cont input:focus, textarea:focus{
  border: 1px solid green;
}

.new-note{
  border-radius: 10px;
  height: 60px;
  width: 200px;
  background: linear-gradient(to right, deepskyblue, dodgerblue);
  color: white;
  font-weight: 500;
  border: none;
  cursor: pointer;
  transition: 0.3s;
}

.new-note:hover{
  background: white;
  color: dodgerblue;
  border: 1px solid dodgerblue;
}

.notes-space{
  padding-top: 30px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.note{
  display: flex;
  gap: 20px;
}
.deadline{
  color: rgba(0, 0, 0, 0.34);
}

.note .text{
  flex-grow: 3;
}

.delete-note{
  border-radius: 10px;
  padding-inline: 20px;
  padding-block: 12px;
  background: #ce0b0b;
  color: white;
  font-weight: 500;
  border: none;
  cursor: pointer;
  transition: 0.3s;
  font-size: 18px;
}

.delete-note:hover{
  background: white;
  color: #ce0b0b;
  border: 1px solid #ce0b0b;
}
</style>
