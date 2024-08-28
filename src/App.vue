<template>
  <div class="shtorka" >
    <div class="popup">
      <div class="popup_header">
        <h2>Изменение задачи</h2>

        <svg @click="closePopup()" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M6 18.9999C5.74414 18.9999 5.48828 18.9022 5.29297 18.7069C4.90234 18.3163 4.90234 17.6835 5.29297 17.2929L17.293 5.29285C17.6836 4.90222 18.3164 4.90222 18.707 5.29285C19.0977 5.68348 19.0977 6.31629 18.707 6.70691L6.70703 18.7069C6.51172 18.9022 6.25586 18.9999 6 18.9999Z" fill="#B6B6B6"/>
          <path d="M18 18.9999C17.7441 18.9999 17.4883 18.9022 17.293 18.7069L5.29297 6.70691C4.90234 6.31628 4.90234 5.68347 5.29297 5.29285C5.6836 4.90223 6.31641 4.90222 6.70703 5.29285L18.707 17.2928C19.0977 17.6835 19.0977 18.3163 18.707 18.7069C18.5117 18.9022 18.2559 18.9999 18 18.9999Z" fill="#B6B6B6"/>
        </svg>

      </div>
      <div class="popup_main">
        <input type="text" v-model="inputPopup">
        <div v-if="taskForChange.status==='Открыт'">
          <button @click="changeStatus('В работу')">В работу</button>
          <button @click="changeStatus('Закрыт')">Закрыть</button>
        </div>
        <div v-if="taskForChange.status==='В работу'">
          <button @click="changeStatus('Открыт')">Отложить</button>
          <button @click="changeStatus('Закрыт')">Закрыть</button>
        </div>
        <div v-if="taskForChange.status==='Закрыт'">
          <button @click="changeStatus('Открыт')">Переоткрыть</button>
        </div>
      </div>
      <div class="popup_footer">
        <button type="button" @click="changeTask()">Применить</button>
        <button type="button" @click="removeTask()">Удалить задачу</button>
      </div>
    </div>
  </div>

  <div class="backContainer">
    <div class="container">

      {{scloud}}

      <h1>{{scloud}}</h1>

      <div class="containerCurrentTasks">
        <div class="block_left">
          <h2>Текущие задачи</h2>

          <div class="counterCurrentTasks">
            <div class="counters">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12.167 22.333C6.56054 22.333 2 17.7724 2 12.1665C2 6.56055 6.56054 2 12.167 2C17.7734 2 22.334 6.56054 22.334 12.1665C22.334 17.7725 17.7734 22.333 12.167 22.333ZM12.167 4C7.66406 4 4 7.66357 4 12.1665C4 16.6694 7.66406 20.333 12.167 20.333C16.6699 20.333 20.334 16.6694 20.334 12.1665C20.334 7.66357 16.6699 4 12.167 4Z" fill="#26A1DE"/>
                <path d="M12.167 16.833C11.6143 16.833 11.167 16.3853 11.167 15.833V12.1665C11.167 11.6143 11.6143 11.1665 12.167 11.1665C12.7197 11.1665 13.167 11.6143 13.167 12.1665V15.833C13.167 16.3853 12.7197 16.833 12.167 16.833Z" fill="#26A1DE"/>
                <path d="M12.1768 9.5C11.624 9.5 11.1719 9.05225 11.1719 8.5C11.1719 7.94775 11.6143 7.5 12.167 7.5H12.1768C12.7295 7.5 13.1768 7.94775 13.1768 8.5C13.1768 9.05225 12.7295 9.5 12.1768 9.5Z" fill="#26A1DE"/>
              </svg>
              Открыто - {{tasks.filter(p=>p.status === "Открыт").length}}
            </div>
            <div class="counters">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12.167 22.333C6.56054 22.333 2 17.7724 2 12.1665C2 6.56055 6.56054 2 12.167 2C17.7734 2 22.334 6.56054 22.334 12.1665C22.334 17.7725 17.7734 22.333 12.167 22.333ZM12.167 4C7.66406 4 4 7.66357 4 12.1665C4 16.6694 7.66406 20.333 12.167 20.333C16.6699 20.333 20.334 16.6694 20.334 12.1665C20.334 7.66357 16.6699 4 12.167 4Z" fill="#FF6600"/>
                <path d="M12.167 16.833C11.6143 16.833 11.167 16.3853 11.167 15.833V12.1665C11.167 11.6143 11.6143 11.1665 12.167 11.1665C12.7197 11.1665 13.167 11.6143 13.167 12.1665V15.833C13.167 16.3853 12.7197 16.833 12.167 16.833Z" fill="#FF6600"/>
                <path d="M12.1768 9.5C11.624 9.5 11.1719 9.05225 11.1719 8.5C11.1719 7.94775 11.6143 7.5 12.167 7.5H12.1768C12.7295 7.5 13.1768 7.94775 13.1768 8.5C13.1768 9.05225 12.7295 9.5 12.1768 9.5Z" fill="#FF6600"/>
              </svg>
              В работе - {{tasks.filter(p=>p.status === "В работу").length}}
            </div>
            <div class="counters">
              <svg width="21" height="21" viewBox="0 0 21 21" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M10.167 20.333C4.56054 20.333 0 15.7724 0 10.1665C0 4.56055 4.56054 0 10.167 0C15.7734 0 20.334 4.56054 20.334 10.1665C20.334 15.7725 15.7734 20.333 10.167 20.333ZM10.167 2C5.66406 2 2 5.66357 2 10.1665C2 14.6694 5.66406 18.333 10.167 18.333C14.6699 18.333 18.334 14.6694 18.334 10.1665C18.334 5.66357 14.6699 2 10.167 2Z" fill="#4DB849"/>
                <path d="M10.167 14.833C9.61426 14.833 9.16699 14.3853 9.16699 13.833V10.1665C9.16699 9.61425 9.61426 9.1665 10.167 9.1665C10.7197 9.1665 11.167 9.61425 11.167 10.1665V13.833C11.167 14.3853 10.7197 14.833 10.167 14.833Z" fill="#4DB849"/>
                <path d="M10.1768 7.5C9.62403 7.5 9.17188 7.05225 9.17188 6.5C9.17188 5.94775 9.61425 5.5 10.167 5.5H10.1768C10.7295 5.5 11.1768 5.94775 11.1768 6.5C11.1768 7.05225 10.7295 7.5 10.1768 7.5Z" fill="#4DB849"/>
              </svg>
              Закрыто - {{tasks.filter(p=>p.status === "Закрыт").length}}
            </div>
          </div>
        </div>


        <div class="block_right">
          <h2>Добавить задачу</h2>
            <form class="formAddTask" @submit.prevent>
              <button type="button" class="btnAddTask" @click="createTask"><span>&mdash;</span><span>&mdash;</span></button>
              <input type="text" v-model="descriptionTask">
              <button class="btnAddTaskMobile" @click="createTask">Добавить задачу</button>
              <span @click="descriptionTask=''" class="resetDescriptionTask">&times</span>
            </form>
        </div>
      </div>


      <div class="blockDeskTask">
        <div class="task_header">
          <div>Задачи</div>
          <div>Статус</div>
        </div>
        <div class="task_main">
          <span v-if="isShowMoreTasks">
            <div v-for='task in this.tasks.filter(p=>p.status === "Открыт").concat(this.tasks.filter(p=>p.status === "В работу")).concat(this.tasks.filter(p=>p.status === "Закрыт"))'><span>{{task.description}}</span>
              <button @click="showPopup(task)">{{task.status}}</button>
            </div>
          </span>
          <span v-else>
            <div v-for='task in this.tasks.filter(p=>p.status === "Открыт").concat(this.tasks.filter(p=>p.status === "В работу")).concat(this.tasks.filter(p=>p.status === "Закрыт")).slice(0,5)'><span>{{task.description}}</span>
              <button @click="showPopup(task)">{{task.status}}</button>
            </div>
          </span>
        </div>
      </div>
      <button v-if="this.tasks.length>5 && !this.isShowMoreTasks" class="showMore" @click="toggle()">Показать ещё <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M12 15.5C11.7441 15.5 11.4883 15.4023 11.293 15.207L6.29297 10.207C5.90234 9.8164 5.90234 9.18359 6.29297 8.79297C6.6836 8.40235 7.31641 8.40234 7.70703 8.79297L12 13.0859L16.293 8.79297C16.6836 8.40234 17.3164 8.40234 17.707 8.79297C18.0977 9.1836 18.0977 9.81641 17.707 10.207L12.707 15.207C12.5117 15.4024 12.2559 15.5 12 15.5Z" fill="#FF6600"/>
      </svg>
      </button>

      <button v-if="this.tasks.length>5 && this.isShowMoreTasks"  class="showMore" @click="toggle()">Скрыть<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M12 15.5C11.7441 15.5 11.4883 15.4023 11.293 15.207L6.29297 10.207C5.90234 9.8164 5.90234 9.18359 6.29297 8.79297C6.6836 8.40235 7.31641 8.40234 7.70703 8.79297L12 13.0859L16.293 8.79297C16.6836 8.40234 17.3164 8.40234 17.707 8.79297C18.0977 9.1836 18.0977 9.81641 17.707 10.207L12.707 15.207C12.5117 15.4024 12.2559 15.5 12 15.5Z" fill="#FF6600"/>
      </svg>
      </button>


    </div>

  </div>


  <div class="container">
    <div>
      <h1>Доска задач</h1>
      <div class="boardTasks">
        <div class="itemBoardTasks">
          <div class="headerBoard">Открыто</div>
          <div class="mainBoard"
               @drop="onDrop($event, 'Открыт')"
               @dragover.prevent
               @dragenter.prevent>
            <div draggable="true" v-for="el in this.tasks.filter(p=>p.status==='Открыт')" @dragstart="startDrag($event, el)" >{{el.description}}</div>
          </div>
        </div>
        <div class="itemBoardTasks">
          <div class="headerBoard">В работе</div>
          <div class="mainBoard"
               @drop="onDrop($event, 'В работу')"
               @dragover.prevent
               @dragenter.prevent>
            <div draggable="true" v-for="el in this.tasks.filter(p=>p.status==='В работу')" @dragstart="startDrag($event, el)" >{{el.description}}</div>
          </div>
        </div>
        <div class="itemBoardTasks">
          <div class="headerBoard">Закрыто</div>
          <div class="mainBoard"
               @drop="onDrop($event, 'Закрыт')"
               @dragover.prevent
               @dragenter.prevent>
            <div draggable="true" v-for="el in this.tasks.filter(p=>p.status==='Закрыт')" @dragstart="startDrag($event, el)">{{el.description}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>


</template>


<script>
import popup from "@/components/popup.vue";
export default {
  components:{popup,},
  data(){
    return{
      scloud: "ToDo List Scloud",
      tasks: JSON.parse(localStorage.getItem('tasks'))??[],
      descriptionTask: "",
      taskForChange: {
        "id":"",
        "description":"",
        "status":""
      },
      inputPopup: "",
      isShowMoreTasks: false,
    }
  },
  methods:{
    toggle(){
      this.isShowMoreTasks = !this.isShowMoreTasks;
    },
    startDrag(evt, el) {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', el.id)
    },
    onDrop(evt, status) {
      const itemID = evt.dataTransfer.getData('itemID')
      const findedTask = this.tasks.find((item) => item.id == itemID)
      const newPosts = this.tasks.map((task) => (
          task.id === findedTask["id"]
              ? {"id":findedTask.id,"description":findedTask.description,"status":status}
              : task
      ));
      this.tasks = newPosts.filter(p=>p.id);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    applytaskdelete(data){
      this.tasks = this.tasks.filter(p=>p.id !== data.id);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    createTask() {
      if (!localStorage.getItem("tasks")) {
        localStorage.setItem("tasks", JSON.stringify([]))
      }
      this.tasks.push({
        "id": Date.now(),
        "description": this.descriptionTask,
        "status": "Открыт"
      });
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    showPopup(task){
      this.taskForChange= JSON.parse(JSON.stringify(task));
      document.querySelector(".shtorka").style.display="flex";
      document.querySelector(".popup").style.display="block";
      document.querySelector(".popup_main input").value=this.taskForChange["description"];
    },
    closePopup(){
      document.querySelector(".shtorka").style.display="none";
      document.querySelector(".popup").style.display="none";
    },
    removeTask(){
      this.closePopup();
      this.$emit('remove', this.taskForChange);
      this.tasks = this.tasks.filter(p=>p.id !== this.taskForChange.id);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    changeTask(){
      const newPosts = this.tasks.map((task) => (
          task.id === this.taskForChange["id"]
              ? {"id":task.id,"description":this.inputPopup,"status":task.status}
              : task
      ));
      this.tasks = newPosts.filter(p=>p.id);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    changeStatus(status){
        const newPosts = this.tasks.map((task) => (
            task.id === this.taskForChange["id"]
                ? {"id":task.id,"description":task.description,"status":status}
                : task
        ));
        this.tasks = newPosts.filter(p=>p.id);
        this.taskForChange["status"]=status;
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
    }
  }
}
</script>



<style scoped>
.drop-zone {
  height: 100px;
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
}

.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
}
h1{
  font-family: 'Montserrat', sans-serif;
  font-size: 32px;
  line-height: 40px;
}
.backContainer{
  background: #f4f4f4;
  padding-bottom: 40px;
}
.container{
  width: 80%;
  margin: 0 auto;
}
.containerCurrentTasks{
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-around;
  margin-top: 50px;
}
.counterCurrentTasks{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  position: relative;
  top: 26px;
}
.container div .block_left,.block_right{
  display: inline-block;
  width: 48%;
  height: 184px;
  background: #fff;
  border-radius: 56px;
}
h2{
  font-family: 'PT Sans Caption',serif ;
  font-size: 24px;
  line-height: 32px;
}
.block_left h2, .block_right h2{
  position: relative;
  top: 22px;
  left: 24px;
}
.counters{
  display: flex;
  align-items: center;
  padding: 12px 18px 12px 18px;
  border-radius: 50px;
  border: 1px solid #ccc;
}
.counters svg{
  margin-right: 6px;
}
.btnAddTask{
  width: 44px;
  height: 44px;
  position: relative;
  left: 1px;
  top: 2px;
  color: white;
  font-size: 24px;
  background: #FF6600;
  border-radius: 100px;
  border: 0;
  margin-right: 16px;
  cursor: pointer;
}
input{
  width: 76%;
  height: 50px;
  border-radius: 22px;
  border: 1px solid #ccc;
  padding-left: 10px;
}
input:hover{
  cursor: pointer;
}
.resetDescriptionTask{
  display: none;
  cursor: pointer;
  position: absolute;
  color: #FF6600;
  right: 80px;
  top: 10px;
  font-weight: 600;
  font-size: 30px;
}
input:hover ~ .resetDescriptionTask{
  display: block;
}
input:focus ~ .resetDescriptionTask{
  display: block;
}
input:focus, button{
  Outline: none;
}
.formAddTask{
  position: relative;
  top: 22px;
  left: 26px;
}
.btnAddTask span:first-child{
  position: absolute;
  transform: rotate(90deg);
  left: 12px;
  top: 10px;
}




.blockDeskTask{
  background: #fff;
  border-radius: 42px;
  padding: 20px;
  margin-top: 58px;
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







.popup svg{
  cursor: pointer;
}
.shtorka{
  display: none;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  position: fixed;
  background: rgba(0,0,0,0.4);
  z-index: 99;
}
.popup{
  display: none;
  width: 50%;
  background: white;
  border-radius: 20px;
  padding: 10px 26px;
}
.popup input{
  width: 96%;
  border: 1px solid #ccc;
  border-radius: 28px;
  padding: 16px;
}
.popup_header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.popup_footer{
  display: flex;
  justify-content: space-between;
}
.popup_footer button{
  padding: 12px 24px 12px 24px;
  margin-bottom: 8px;
  cursor: pointer;
  border-radius: 20px;
  font-weight: 600;
}
.popup_footer button:first-child{
  background: #FF6600;
  color: white;
  border: 0;
}
.popup_footer button:last-child{
  border: 2px solid #FF6600;
  background: white;
  color: #FF6600;
}
.popup_main div{
  border-top: 3px solid #ccc;
  margin-top: 24px;
}
.popup_main div button{
  margin: 20px;
  border: 0;
  border-radius: 27px;
  padding: 10px 24px;
  cursor: pointer;
}
.btnAddTaskMobile{
  display: none;
  width: 84%;
  background: #FF6600;
  color: #FFF;
  border: 0;
  border-radius: 16px;
  padding: 8px 0;
  margin: 16px 0;
}








.boardTasks{
  display: flex;
  justify-content: space-between;
}
.itemBoardTasks{
  width: 32%;
}
.mainBoard{
  background: #f4f4f4;
  border-radius: 12px;
  padding: 20px;
}
.mainBoard div{
  padding: 16px;
  background: white;
  border-radius: 12px;
  margin-bottom: 10px;
  font-weight: 600;
}
.headerBoard{
  text-align: center;
  margin-bottom: 20px;
  border-radius: 18px;
  font-weight: 600;
  background: #f4f4f4;
  padding: 14px;
  width: 80px;
}

.showMore{
  background: white;
  color: #FF6600;
  border-radius: 30px;
  border: 1px solid #FF6600;
  cursor: pointer;
  font-weight: 600;
  display: flex;
  align-items: center;
  padding: 8px 20px;
  margin-top: 20px;
}
@media (min-width: 993px) and (max-width: 1220px) {
  .container{
    width: 90%;
  }
  .formAddTask input{
    width: 68%;
  }
  .counters{
    padding: 12px 8px 12px 8px;
  }
  .resetDescriptionTask{
    right: 90px;
  }
}
@media (min-width: 641px) and (max-width: 992px) {
  .containerCurrentTasks{
    flex-direction: column;
  }
  .container div .block_left,.block_right{
    width: 100%;
  }
  .container div .block_left{
    margin-bottom: 40px;
  }
  .resetDescriptionTask{
    display: block;
    right: 15%;
  }
}
@media (min-width: 320px) and (max-width: 640px) {
  .resetDescriptionTask{
    display: block;
  }
  .containerCurrentTasks{
    flex-direction: column;
  }
  .container div .block_left,.block_right{
    width: 100%;
  }
  .container div .block_left{
    margin-bottom: 40px;
  }
  .container{
    width: 96%;
  }
  .counterCurrentTasks{
    flex-direction: column;
    align-items: center;
  }
  .counters{
    padding: 8px;
    width: 80%;
    justify-content: center;
    margin-bottom: 10px;
  }
  .container div .block_left{
    height: 272px;
  }
  .block_right{
    height: 234px;
  }
  .formAddTask{
    display: flex;
    flex-direction: column;
  }
  .formAddTask button{
    order: 2;
  }
  .btnAddTask{
    display: none;
  }
  .formAddTask input{
    width: 80%;
    order: 1;
  }
  .btnAddTaskMobile{
    display: block;
  }
  .task_header div:nth-child(2){
    display: none;
  }
  .blockDeskTask{
    background: none;
  }
  .task_main span{
    padding: 12px;
    font-weight: 600;
  }
  .task_main span div{
    flex-direction: column;
    background: white;
    border-radius: 12px;
    border: 0;
    margin-bottom: 20px;
  }
}
</style>