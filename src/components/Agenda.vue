<template>
  <div class="agenda">
    <div>
      <img src="~src/assets/world_icon.png" width=40 height=40>
      <input @keydown.enter="keydownEnter($event)" v-model="agenda.title" placeholder="Type a new agenda" type="text">
    </div>
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
  /*margin: 5px 0px;*/
}

.agenda > div {
  padding: 5px;
  margin: 10px 0px;
  border-radius: 2px;
}

.agenda > div:hover {
  background: rgba(0,0,0,0.05);
}

.agenda > ul {
  flex-direction: column;
  padding-left: 40px;
  margin-left: 5px;
}

.agenda > div > img {
  width: 20px;
  height: 20px;
}

.agenda > div > input {
  flex: 1;
  margin-left: 20px;
  font-size: 14px;
  letter-spacing: 0.6px;
}

.paper__main > ul > .agenda > div {
  margin: 20px 0px;
}

.paper__main > ul > .agenda > div > img {
  width: 40px;
  height: 40px;
}

.paper__main > ul > .agenda > div > input {
  margin-left: 20px;
  font-size: 18px;
  letter-spacing: 0.6px;
}

</style>
