<template>
  <div :class="['agenda', {'agenda--root': root}, {'close': close}, , {'agenda--top': (address.length === 2)}]">
    <div v-if="!root" class="agenda__title">
      <!-- <p>{{address}}</p> -->
      <div class="agenda__i">
        <div class="agenda__i--child" @click="addAgenda(0)"></div>
        <div class="agenda__i--result" @click="result = !result"></div>
      </div>
      <input @keydown.enter="keydownEnter($event)" v-model="agenda.title" placeholder="Type a new agenda" type="text">
    </div>
    <div class="agenda__children">
      <div class="agenda__line" @click="close = !close">
        <div></div>
      </div>
      <ul>
        <agenda v-for="(agenda, i) in agenda.children" :agenda="agenda" :i="i" :root="false" :focus.sync="focus"></agenda>
        <div class="agenda-add" v-if="agenda.children.length">
          <div class="agenda-add__button" @click="addAgenda(agenda.children.length)"></div>
        </div>
      </ul>
    </div>
    <div class="agenda__result" v-show="result">
      <div class="agenda__result__button"></div>
      <div class="agenda__result__text" contentEditable="true">
        <p>ここに結果をかきましょー、ここに結果をかきましょー、ここに結果をかきましょー、ここに結果をかきましょー</p>
      </div>
    </div>
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
  data () {
    return {
      close: false,
      result: false
    }
  },
  methods: {
    keydownEnter: function (event) {
      event.shiftKey ? this.addAgenda() : this.$parent.addAgenda(this.i)
    },
    addAgenda: function (i) {
      this.agenda.children.splice(i + 1, 0, { title: '', children: [] })
      // this.focus = this.address.concat([i + 1])
    }
  },
  watch: {
    'focus': {
      handler: function (val, oldVal) {
        console.log(val)
        // console.log(this.address)
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

.close .agenda {
  pointer-events: none;
}

.agenda:hover {
  /*box-shadow: 0 1px  4px rgba(0,0,0,0.2);*/
}

.agenda--root:hover {
  box-shadow: 0 1px  4px rgba(0,0,0,0.0);
}

.agenda--top {
  margin: 10px 0px;
}

.agenda__title {
  margin: 5px 0px;
  border-radius: 2px;
  background: rgba(0,0,0,0.0);
  position: relative;
  border-radius: 100px;
}

.agenda--top > .agenda__title {
  margin: 10px 0px;
}

.close > .agenda__children .agenda__title {
  margin: 0px 0px;
}

.agenda__title:hover {
  background: rgba(0,0,0,0.05);
}

.agenda__title > p {
  position: absolute;
  font-size: 9px;
  font-weight: 700;
  color: rgba(0,0,0,0.3);
  background: rgba(255,255,255,0.2);
  opacity: 0.0;
}

.agenda__title > .agenda__i {
  width: 20px;
  height: 20px;
  top: 5px;
  left: 5px;
  position: absolute;
  cursor: pointer;
}

.agenda__title > .agenda__i:hover {
  z-index: 100;
}

.agenda__title > .agenda__i:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url("~src/assets/world_icon.png");
  background-color: #fff;
  background-size: 100%;
  border-radius: 50%;
}

.agenda__title > .agenda__i:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(255,255,255,0.8);
  box-shadow: 0 2px 5px rgba(0,0,0,0.0);
  border-radius: 50%;
}

.agenda__title > .agenda__i:hover:before {
  top: -22px;
  left: -22px;
  bottom: -22px;
  right: -22px;
  box-shadow: 1px 1px 2px rgba(0,0,0,0.06);
}

.agenda--top > .agenda__title > .agenda__i:hover:before {
  top: -44px;
  left: -44px;
  bottom: -44px;
  right: -44px;
  box-shadow: 2px 2px 5px rgba(0,0,0,0.06);
}


.agenda--top > .agenda__title > .agenda__i {
  width: 40px;
  height: 40px;
}

.close > .agenda__children .agenda__title > .agenda__i {
  top: 2px;
  left: 2px;
  width: 6px;
  height: 6px;
  box-shadow: 0 0 0 1px #f26d25 inset;
  border-radius: 50%;
}

.agenda__i--child {
  width: 10px;
  height: 10px;
  top: 5px;
  left: 5px;
  background-color: #fff;
  background-image: url("~src/assets/plus_icon.png");
  background-size: 100%;
  position: absolute;
  border-radius: 50%;
}

.agenda__i--child:hover {
  box-shadow: 0 0 0 4px rgba(244, 108, 11, 0.2);
}

.agenda__i:hover > .agenda__i--child {
  top: 20px;
  left: 20px;
}

.agenda--top > div > div > .agenda__i--child {
  width: 20px;
  height: 20px;
  top: 10px;
  left: 10px;
}

.agenda--top > div > .agenda__i:hover > .agenda__i--child {
  top: 40px;
  left: 40px;
}

.close > .agenda__children .agenda__i--child {
  opacity: 0.0;
}

.agenda__i--result {
  width: 10px;
  height: 10px;
  top: 5px;
  left: 5px;
  background-color: #fff;
  background-image: url("~src/assets/check_icon.png");
  background-size: 100%;
  position: absolute;
  border-radius: 50%;
}

.agenda__i--result:hover {
  box-shadow: 0 0 0 4px rgba(108, 212, 87, 0.2);
}

.agenda__i:hover > .agenda__i--result {
  top: 26px;
  left: 5px;
}

.agenda--top > div > div > .agenda__i--result {
  width: 20px;
  height: 20px;
  top: 10px;
  left: 10px;
}

.agenda--top > div > .agenda__i:hover > .agenda__i--result {
  top: 52px;
  left: 10px;
}

.close > .agenda__children .agenda__i--result {
  opacity: 0.0;
}



.agenda__title > input {
  flex: 1;
  padding: 5px 5px 5px 40px;
  height: 30px;
  font-size: 14px;
  /*letter-spacing: 0.1rem;*/
}

.agenda--top > .agenda__title > input {
  font-size: 18px;
  padding: 5px 5px 5px 60px;
  height: 50px;
}

.close > .agenda__children .agenda__title > input {
  font-size: 10px;
  height: 10px;
  padding: 0px 5px 0px 15px;
}


.agenda__children {
  flex-direction: row;
}

.agenda__line {
  width: 20px;
  background: rgba(0,0,0,0.0);
  margin: 0 5px;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
}

.agenda--top > .agenda__children > .agenda__line {
  width: 40px;
}

.agenda--root > .agenda__children > .agenda__line {
  display: none;
}

.close > .agenda__children .agenda__children .agenda__line {
  width: 6px;
  margin: 0;
}

.agenda__children > .agenda__line > div {
  flex: 1;
  width: 2px;
  background: #ddd;
  border-radius: 1px;
}

.agenda__children > .agenda__line:hover > div {
  flex: 1;
  width: 4px;
  background: #ccc;
  border-radius: 2px;
}

.close > .agenda__children .agenda__children .agenda__line > div {
  opacity: 0;
}

.agenda__children > ul {
  flex: 1;
  flex-direction: column;
}

.agenda--root > ul {
  padding-left: 0px;
  margin-left: 0px;
  position: relative;
}

.agenda-add {
  width: 100%;
  height: 30px;
  margin: 5px 0;
  position: relative;
}

.agenda--root > div > ul > .agenda-add {
  height: 70px;
  margin: 10px 0;
}

.agenda-add__button {
  width: 20px;
  height: 20px;
  top: 5px;
  left: 5px;
  position: absolute;
  cursor: pointer;
  background-image: url("~src/assets/plus_big_icon.png");
  background-color: #fff;
  background-size: 100%;
  border-radius: 50%;
}

.agenda--root > div > ul > .agenda-add > .agenda-add__button {
  width: 40px;
  height: 40px;
  top: 15px;
  left: 5px;
}

.agenda-add__button:hover {
  box-shadow: 0 0 0 4px rgba(244, 108, 11, 0.2);
}

.close .agenda-add {
  height: 0px;
  margin: 0 0;
  opacity: 0;
}

.agenda__result {
  width: 100%;
  min-height: 30px;
  margin: 5px 0;
  background: #eee;
  position: relative;
  border-radius: 15px;
  /*display: none;*/
}

.agenda--top > .agenda__result {
  min-height: 70px;
  margin: 10px 0;
  border-radius: 25px;
}

.agenda--root > .agenda__result {
  display: none;
}

.agenda__result__button {
  width: 20px;
  height: 20px;
  top: 5px;
  left: 5px;
  position: absolute;
  cursor: pointer;
  background-image: url("~src/assets/check_big_icon.png");
  background-color: #fff;
  background-size: 100%;
  border-radius: 50%;
}

.agenda--top > .agenda__result > .agenda__result__button {
  width: 40px;
  height: 40px;
  top: 5px;
  left: 5px;
}

.agenda__result__text {
  width: 100%;
  padding: 5px 5px 5px 40px;
  flex-direction: column;
}

.agenda--top > .agenda__result > .agenda__result__text {
  padding: 10px 10px 10px 60px;
}

.agenda__result__text > p {
  font-size: 14px;
  line-height: 20px;
  flex: 1;
  display: block;
}

.agenda--top > .agenda__result > .agenda__result__text > p {
  font-size: 18px;
  line-height: 30px;
}

</style>
