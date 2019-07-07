<template>
    <div class="todolist">
        <TodoForm @add="addItem"/>
        <ul>
            <ListItem  v-for="task in tasks" @rm="removeItem" :task="task" :key="task.id"/>
        </ul>
        <button v-if="seen" @click="clearAll">Удалить все</button>
    </div>
</template>

<script>
import TodoForm from './TodoForm.vue'
import ListItem from './ListItem.vue'

export default {
  name: 'TodoList',
  components: {
    TodoForm, ListItem
  },
  data(){
    return{
        tasks: [],
        seen: false
    }
  },
  methods: {
      addItem(item){
        item.id = this.tasks.length ? this.tasks[this.tasks.length - 1].id + 1 : item.id++;
        this.tasks.push({...item});
      },
      removeItem(removeItemID){
          this.tasks = this.tasks.filter(task => task.id !== removeItemID);
      },
      clearAll(){
        this.tasks = [];
      },
  },
  mounted: function(){
      this.tasks = localStorage.getItem("tasks")? JSON.parse(localStorage.getItem("tasks")) : []; //извлекаем массив из хранилища
      let id = 0;
      this.tasks.map(item => item.id = id++);
  },
  updated: function(){
    localStorage.setItem("tasks", JSON.stringify(this.tasks));//записываем массива в хранилище
    this.seen = this.tasks.length ? true : false;
  }
}
</script>

<style scoped>
 .todolist{
   display: flex;
   flex-direction: column;
  background: #fff;
  padding: 30px;
  margin-top: 30px;
  position: relative;
  border-radius: 10px;
  box-shadow: 0 0 13px rgba(0, 0, 0, 0.2);
}
ul{
  margin: 0%;
  padding: 0%;
}
button{
  margin-top: 15px; 
  border: none;
  padding: 5px 40px;
  outline: none;
  cursor: pointer;
  font-weight: 400;
  border-radius: 4px;
  border: 1px solid #6c757d;
  font-size: 14px;
  color: #6c757d;
  background-color: transparent;
  transition: all .2s;
  }
    button:hover{
    background-color: #6c757d;
    color: #fff;
  }
</style>
