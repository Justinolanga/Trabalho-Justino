<template>
  <q-page class="bg-grey-3 column">
   <div class="row q-pa-sm bg-color-primary">
   <q-input v-model="newTask" @keyup.enter="addTask" class="col" square filled bg-color="white"  placeholder="Adicionar"  dense>


        <template v-slot:append>
          <q-btn
            @click="addTask"
          round dense flat icon="add" />
        </template>
      </q-input>
    </div>

    <div class="q-pa-md">
    <div class="q-gutter-sm">
    <q-list class="bg-white">

      <q-item v-for="(task,index) in tasks"
      :key="task.title"
      @click="task.done=!task.done"
      :class="{'done bg-blue-1':task.done}"
      clickable
      v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="color" color="primary" />
        </q-item-section>
        <q-item-section>
         <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>

        <q-item-section
        v-if="task.done"
        side><q-btn @click.stop="deleteTask(index)" flat round dense color="primary" icon="delete" />
        </q-item-section>
      </q-item>


    </q-list>
    </div>


  </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
   data(){

return{
  newTask:'',

  tasks:[

  ]
}
},
methods:{
  deleteTask(index){

  this.$q.dialog({
  title:'Mensagem',
  message: 'Continuar?',
  cancel: true,
  persistent: true

  }).onOk(() =>{
    this.tasks.splice(index, 1)
    this.$q.notify('Eliminado')

  })

  },
  addTask(){
     this.tasks.push({
     title: this.newTask,
     done: false
     })
     this.newTask = ''
  }
}


})
</script>
