<template>
  <q-page class="bg-grey-3 column">
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
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          title: 'Assitir Cblol',
          done: false,
        },
        {
          title: 'Assitir o jogo do mengão',
          done: false,
        },
        {
          title: 'Ir ao cinema',
          done: false,
        },
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
</style>