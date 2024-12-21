<script>

export default{
  data(){
    return{
    }
  },
  props:{
    taskForChange:{
      type: Object,
      required: true
    }
  },
  computed: {
    inputPopup: {
      get() {
        return this.taskForChange.description;
      },
      set(value){
        this.taskForChange.description=value
      }
    },
  },
  methods:{
    closePopup(){
      document.querySelector(".shtorka").style.display="none";
      document.querySelector(".popup").style.display="none";
    },
    removeTask(){
      this.closePopup();
      this.$emit('removeTask', this.taskForChange);
    },
    changeTask(){
      this.taskForChange["description"]=this.inputPopup
      this.$emit('editTask', this.taskForChange);
    },
    changeStatus(status){
      this.taskForChange["status"]=status
      this.$emit('editStatusTask', this.taskForChange);
    }
  }
}
</script>

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

</template>

<style scoped>
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
</style>