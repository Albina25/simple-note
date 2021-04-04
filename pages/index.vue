<template>
  <div class="task-table">
  <table class="task-positions">
    <thead>
      <tr>
        <th></th>
        <th>№</th>
        <th>название <input type="text" v-modal="task.title"></th>
        <th>дата завершения</th>
        <th>статус</th>
        <th>действие</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(task,index) of filteredList()" :key="task.id" @click="openTask(index)">
        <td><input type="checkbox" id="task.id" value="task.id"></td> 
        <td  v-for="(item, name, index) of task" :key="index" v-show ="visibleTd.includes(name)">{{item}}</td>
        
       
        <td><button class="table-btn" @click.stop="completeTask(index)">завершить</button></td>
      </tr>
    </tbody>
  </table>
   <dialog ref="taskModal">
      <form method="dialog" @submit.prevent="saveTask">
      <header>задача
      <button type="button" class="close-btn" @click="closeModal">x</button>
      </header>
      <label>название
      <input type="text" placeholder="название" v-model="taskForm.title" required>
      </label>
      <label>описание
      <input type="text" placeholder="описание" v-model="taskForm.description">
      </label>
      <label>дата выполнения
      <input type="datetime-local" placeholder="дата" v-model="taskForm.dateToComplete">
      </label>
      <label>адрес
      <input type="text" placeholder="адрес" v-model="taskForm.address">
      </label>
      <footer>
      <button type="button" @click="resetTask()">сброс</button>
      <button type="button" @click="completeTask()">завершить</button>
      <button type="submit" @click="saveTask()">сохранить</button>
      </footer>
      </form>
    </dialog>
   </div>
</template>

<script>
export default {
  name: 'index',
  head () {
    return {
      title: 'Задачи'
    }
  },
  layout: 'foondement',
  data: () => ({
  taskForm: {
    id: null,
    title: '',
    description: '',
    address: null,
    createdAt: null,
    dateToComplete: null,
    status: 'открыт',
  },
  
  checkedId: [],
  visibleTd:['id', 'title', 'dateToComplete', 'status'],
  tasks: [
      { id: 1, title: 'Сходить в магазин', description: 'купить фрукты', address: 'Магнит', dateToComplete: null, status: 'открыт' },
      { id: 2, title: 'Проверить уроки', description: 'матем', address:'дом', dateToComplete: null, status: 'открыт' }
    ]
  }),
  methods: {
  openModal () {
    
     this.$refs.taskModal.showModal();
      },
  closeModal () {
     
     this.$refs.taskModal.close();
     
  },
 resetTask () {
 const index = this.tasks.findIndex(e => e.id === this.taskForm.id);
 //for (var value in this.tasks[index]) {
  // delete this.tasks[index].value;}
  //for (var key of this.tasks[index]) 
  //   delete this.tasks[index][key];}
   
   this.taskForm.title = '';
  },
  saveTask () {
    
    if (!this.taskForm.id) {
    this.taskForm.id = this.tasks.length + 1;
    this.tasks.push(this.taskForm);
    } else {
    const index = this.tasks.findIndex(e => e.id === this.taskForm.id);
    this.tasks[index]=this.taskForm;
    }
    
    this.closeModal();
   
  },
  
  completeTask (index) {
  if (index != undefined) {
    this.tasks[index].status = 'завершен';
    
    } else {
      this.taskForm.status = 'завершен';
    }
   
    this.closeModal();
    
  },
  openTask (index) {
     this.taskForm = this.tasks[index];
     this.openModal();
    
     
  },
  

  filteredList() {
   
  return this.tasks.filter(task => task.title.includes(task.title))
  }
},
               
   mounted () {
      this.$nuxt.$on('showDialog', this.openModal)
      //  this.$nuxt.$on('completeTask', this.completeTask)
       }
}
</script>

<style lang="scss">
.task-table {
 width: 100%;
 height: calc(100% - 60px);
}
 .task-positions {
 border: 3px solid #E7E5DD;
}
</style>
