<template>
  <div>
    <div class="formtodo">
      <div class="formHeader">
        <h2>Список задач</h2>
        <img src="../assets/clipboard.png" width="30" height="30" alt="clipboard">
      </div>
      <input  type="text" v-model="task.text" placeholder="Введите текст" :class="{ errClass: errMsgText }">
      <span>{{errMsgText}}</span>
      <input  type="text" v-model="task.time" placeholder="Введите время (**:**)" :class="{ errClass: errMsgTime }">
      <span>{{errMsgTime}}</span>
      <button @click="addTask">Добавить</button>
    </div>
  </div>
</template>

<script>
let str = /^([0,1][0-9]|2[0-3]):[0-5][0-9]$/;

export default {
  name: 'TodoForm',
  data() {
    return {
      task:{
        id: 0,
        text: "",
        time: "",
      },
      errMsgText: "",
      errMsgTime: "",
    }
  },
  methods: {
    addTask(){
      if(!this.checkData(this.task)){
          this.$emit('add', this.task);
          //очищаем форму
          this.task.text = "";
          this.task.time = "";
          this.errMsgText = "";
          this.errMsgTime = "";
      }
    },
    checkData(item){    //валидация данных
      let error = false;
      if(item.text === ""){
        this.errMsgText = "Заполните поле";
        error = true;
      }else this.errMsgText = "";
      if(item.time === ""){
        this.errMsgTime = "Заполните поле";
        error = true;
      }
      else{
        if(item.time.search(str) == -1){
          this.errMsgTime = "Введите корректное время";
          error = true;
        }else{
          this.errMsgTime = "";
        }
      }
      return error;
    }
  }
  }
</script>

<style scoped>
  .formtodo{
  display: flex;
  flex-direction: column;
  background-color: #fff;
}
.formHeader{
  display: inherit;
  align-items: center;
  justify-content: center;
}
  button, input {
  border-radius: 4px;
  border: none;
  margin: 15px 0;
  padding: 16px 40px;
  outline: none;
  transition: all .2s;
}

input{
  background: #efefef;
  font-size: 14px;
  transition: all 0.2s;
}

input:focus{
  background-color: #ddd;
}
  button{
    cursor: pointer;
    font-weight: 400;
    border: 1px solid #6c757d;
    font-size: 16px;
    line-height: 1.5;
    color: #6c757d;
    background-color: transparent;
  }
    button:hover{
    background-color: #6c757d;
    color: #fff;
  }
  span{
    color: crimson;
    font-size: 14px;
  }
  .errClass{
    border: 2px solid crimson;
  }

</style>