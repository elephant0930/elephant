<template>
  <div :class="['agenda', { 'agenda--root': root}]">
    <div v-if="!root">
      <p>{{address}}</p>
      <img src="~src/assets/world_icon.png" width=40 height=40>
      <input @keydown.enter="keydownEnter($event)" v-model="agenda.title" placeholder="Type a new agenda" type="text">
    </div>
    <ul>
      <agenda v-for="(agenda, i) in agenda.children" :agenda="agenda" :i="i" :root="false" :focus.sync="focus"></agenda>
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
  computed: {
    address: function () {
      if (this.$parent.address) {
        return this.$parent.address.concat([this.i])
      } else {
        return [this.i]
      }
    }
  },
  props: ['agenda', 'i', 'root', 'focus'],
  methods: {
    keydownEnter: function (event) {
      event.shiftKey ? this.addAgenda() : this.$parent.addAgenda(this.i)
    },
    addAgenda: function (i) {
      this.agenda.children.splice(i + 1, 0, { title: '', children: [] })
      this.focus = this.address.concat([i + 1])
    }
  },
  watch: {
    'focus': {
      handler: function (val, oldVal) {
        console.log(val)
        console.log(this.address)
      }
    }
  }
}
</script>

<style scoped>

.agenda {
  flex-direction: column;
  position: relative;
}

.agenda:hover {
  /*box-shadow: 0 1px  4px rgba(0,0,0,0.2);*/
}

.agenda--root:hover {
  box-shadow: 0 1px  4px rgba(0,0,0,0.0);
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

.agenda > div > p {
  position: absolute;
  font-size: 9px;
  font-weight: 700;
  color: rgba(0,0,0,0.3);
  background: rgba(255,255,255,0.2);
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

.agenda--root > ul {
  padding-left: 0px;
  margin-left: 0px;
}

.agenda--root > ul > .agenda > div {
  margin: 20px 0px;
}

.agenda--root > ul > .agenda > div > img {
  width: 40px;
  height: 40px;
}

.agenda--root > ul > .agenda > div > input {
  margin-left: 20px;
  font-size: 18px;
  letter-spacing: 0.6px;
}

</style>
