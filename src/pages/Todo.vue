<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        @keyup.enter="addTask"
        filled
        v-model="newTask"
        placeholder="Add Task"
        dense
        bg-color="white"
        class="col"
        square
      >
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click.prevent="addTask" />
        </template>
      </q-input>
    </div>
    <q-list separator bordered class="bg-white">
      <q-item
        v-ripple
        v-for="(task, index) in tasks"
        :key="index"
        @click="task.done = !task.done"
        clickable
        :class="{'done bg-blue-1': task.done}"
      >
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" class="no-pointer-events" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn flat round dense color="primary" icon="delete" @click.stop="deleteTask(index)" />
        </q-item-section>
      </q-item>
    </q-list>
    <div class="no-tasks absolute-center" v-if="!tasks.length">
      <q-icon name="check" size="100px" color="primary" />
      <div class="text-h5 text-primary text-center">No tasks</div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        // {
        //   title: 'Assitir Cblol',
        //   done: false,
        // },
        // {
        //   title: 'Assitir o jogo do mengão',
        //   done: false,
        // },
        // {
        //   title: 'Ir ao cinema',
        //   done: false,
        // },
      ]
    }
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Would you like to delete the task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1) //delete one item (second param) at the index 
        this.$q.notify('Task deleted')
      })
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false
      })

      this.newTask = ''
    }
  }
}
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}
.no-tasks {
  opacity: 0.5;
}
</style>