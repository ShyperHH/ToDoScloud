<script>
export default {
  data(){
    return{
      tasks: JSON.parse(localStorage.getItem('tasks'))??[]
    }
  },
  methods:{
    showPopup(task){
      this.taskForChange= JSON.parse(JSON.stringify(task));
      document.querySelector(".shtorka").style.display="flex";
      document.querySelector(".popup").style.display="block";
      document.querySelector(".popup_main input").value=this.taskForChange["description"];
      this.$emit('toggle', this.taskForChange);
    }
  }
}
</script>

<template>
  <div class="blockDeskTask">
    <div class="task_header">
      <div>Задачи</div>
      <div>Статус</div>
    </div>
    <div class="task_main">
      <div v-for='task in tasks.slice(0, 5)'><span>{{task.description}}</span>
        <button @click="showPopup(task)">{{task.status}}</button></div>
    </div>
  </div>
</template>

<style scoped>
.blockDeskTask{
  position: relative;
  top: 60px;
  background: #fff;
  border-radius: 42px;
  padding: 20px;
}
.task_header, .task_main div{
  display: flex;
  justify-content: space-between;
}
.task_header div{
  font-weight: 900;
  font-size: 18px;
  padding: 0 28px 10px 16px;
}
.task_main div{
  margin: 0 14px 0 14px;
  padding: 10px 2px;
}
.task_main div:not(:last-child){
  border-bottom: 1px solid #ccc;
}
.task_main button{
  border: 0;
  background: #f4f4f4;
  border-radius: 16px;
  padding: 6px 14px;
}
</style>