<template>
  <div class="task-table">
  <table>
    <thead>
      <tr>
        <td>статус</td>
        <td>название</td>
        <td>описание</td>
        <td>адрес</td>
        <td>дата завершения</td>
        <td>дата создания</td>
        <td>действие</td>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(task,index) of tasks" :key="task.id" @click=openTask(index)>
        <td v-for="(item, index) of task" :key="index">{{item}}</td>
        <td><button class="table-btn" @click.stop="completeTask">завершить</button></td>
      </tr>
    </tbody>
  </table>
   <dialog ref="taskModal">
      <form method="dialog" @submit.prevent="saveTask">
      <header>задача
      <button type="button" class="close-btn">x</button>
      </header>
      <label>название
      <input type="text" placeholder="название" v-model="taskForm.title" required>
      </label>
      <label>описание
      <input type="text" placeholder="описание" v-model="taskForm.description">
      </label>
      <label>дата выполнения
      <input type="datetime-local" placeholder="дата" v-model="taskForm.dateToComplete" requared>
      </label>
      </label>
      <label>адрес
      <input type="text" placeholder="адрес" v-model="taskForm.address">
      </label>
      <footer>
      <button type="reset">сброс</button>
      <button type="button" @click="completeTask()">завершить</button>
      <button type="submit">сохранить</button>
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
    status: null,
    },
  
  tasks: [
      { id: 1, title: 'Сходить в магазин', description: 'Купить фрукты, хлеб', address: null, createdAt: null, dateToComplete: null, status: null },
      { id: 2, title: '', description: '', address: null, createdAt: null, dateToComplete: null, status: null }
    ]
  }),
  methods: {
  openModal () {
     this.$refs.taskModal.showModal()
      },
  closeModal () {
     this.$refs.taskModal.close()
      },
  saveTask () {
    if (!this.id) {
    this.taskForm.id = this.tasks.length + 1;
    this.tasks.push(this.taskForm);
    this.closeModal();
   } 
      },
  completeTask (i) {
  if (i != undefined) {
   console.log({'i': i});
    this.tasks[i].status = 1
    } else {
      this.taskForm.status = 1
    }
   
    this.closeModal();
  },
  openTask (index) {
     this.taskForm = this.tasks[index];
      this.openModal();
  }
  },

   mounted () {
    console.log(this.$refs)
       this.$nuxt.$on('showDialog', this.openModal)
       }
}
</script>

<style lang="scss">
.task-table {
 width: 100%;
 height: calc(100% - 60px);
}
</style>
