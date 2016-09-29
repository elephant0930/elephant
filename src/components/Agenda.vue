<template>
  <div class="agenda">
    <input @keydown.enter="keydownEnter($event)" v-model="agenda.title" type="text">
    <ul>
      <agenda v-for="agenda in agenda.children" :agenda="agenda"></agenda>
    </ul>
  </div>
</template>

<script>
import Agenda from './Agenda.vue'

export default {
  name: 'agenda',
  components: {
    Agenda
  },
  props: ['agenda'],
  methods: {
    keydownEnter: function (event) {
      event.shiftKey ? this.addAgenda() : this.$parent.addAgenda()
    },
    addAgenda: function () {
      this.agenda.children.push({
        title: 'new agenda',
        children: []
      })
    }
  }
}
</script>

<style scoped>

.agenda {
  flex-direction: column;
  margin: 5px 0px;
}

.agenda > ul {
  flex-direction: column;
  padding-left: 30px;
}
</style>
