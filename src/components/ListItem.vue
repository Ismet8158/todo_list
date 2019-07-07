<template>
  <li>
      <div class="todoTask">
        <p>{{task.text}}</p>
        <span>{{task.time}}</span>
      </div>
      <img @click="remove" src="../assets/remove.png" width="27" height="27" class="delete">
  </li>
</template>

<script>

export default {
  name: 'ListItem',
  props: {
      task: Object
  },
  methods: {
    remove() {
      this.$emit('rm', this.task.id);
    }
  }
}
</script>

<style scoped>
  li{
    list-style-type: none;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 13px;
    transition: all 0.2s;
  }
  li:hover {
    background-color: #efefef;
    border-radius: 4px;
  }
  div{
    display: inherit;
    align-items: inherit;
  }
  li:hover .delete{
    visibility: visible;
  }
  img{
    cursor: pointer;
  }
  .delete{
    visibility: hidden;
    margin: 10px;
  }
  .todoTask{
    flex-direction: column;
    align-items: flex-start;
    margin-left: 12px;
  }
  p{
    font-size: 16px;
    word-break: break-all;
  }
  span{
    color: #6c757d;
    font-size: 12px;
  }
  .completeClass{
    text-decoration: line-through;
  }
</style>