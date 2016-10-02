<template>
  <div id="app">
    <div class="nav"></div>
    <div class="list"></div>
    <div class="content">
      <div class="content__header">
        <p>改善相談</p>
      </div>
      <ul>
        <li class="paper">
          <div class="paper__header">
            <div class="paper__header__users">
              <ul>
                <li>
                  <img src="~src/assets/user_keima.jpg" alt="">
                </li>
                <li>
                  <img src="~src/assets/user_wasabi.jpg" alt="">
                </li>
                <li>
                  <img src="~src/assets/user_terayama.jpg" alt="">
                </li>
              </ul>
            </div>
            <div>{{focus}}</div>
          </div>
          <div class="paper__main">
            <agenda :agenda="agenda" :root="true" :i="0" :focus.sync="focus"></agenda>
          </div>
        </li>
        <li class="paper">
          <div class="paper__header">
            <div>
              <ul>
                <li>
                  <img src="" alt="">
                </li>
                <li>
                  <img src="" alt="">
                </li>
                <li>
                  <img src="" alt="">
                </li>
              </ul>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Agenda from './components/Agenda'

export default {
  components: {
    Agenda
  },
  data () {
    return {
      agenda: {
        title: '',
        children: [
          {
            title: '',
            children: []
          }
        ]
      },
      focus: {}
    }
  }
}
</script>

<style>

@import './reset.css';

html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  width: 100%;
}

#app {
  width: 100%;
  height: 100%;
  flex-direction: row;
}

.nav {
  width: 60px;
  height: 100%;
  background: #2b405c;
}

.list {
  width: 60px;
  height: 100%;
  background: #fff;
  z-index: 100;
  box-shadow: 1px 0 3px rgba(0,0,0,0.08);
}

.content {
  height: 100%;
  background: #f1f1f1;
  flex: 1;
  flex-direction: column;
}

.content__header {
  width: 100%;
  height: 60px;
  background: #fff;
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
  z-index: 70;
  justify-content: center;
  align-items: center;
}

.content > ul {
  width: 100%;
  flex: 1;
  padding: 30px 90px;
  overflow-y: auto;
  overflow-x: hidden;
}

.content > ul > li.paper {
  flex-direction: column;
  width: 100%;
  background: #fff;
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
  margin: 30px 0;
  overflow: hidden;
}

.paper__header {
  width: 100%;
  height: 60px;
  background: #fff;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12);
  z-index: 60;
  justify-content: flex-start;
  align-items: center;
}

.paper__header__users {
  padding: 0 10px;
}

.paper__header__users > ul {
  padding: 0 5px;
}

.paper__header__users > ul > li {
  margin: 0 5px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 0 0 0.5px rgba(0,0,0,0.2);
}

.paper__header__users > ul > li > img {
  width: 20px;
  height: 20px;
}

.paper__main {
  width: 100%;
  flex: 1;
  padding: 60px;
  flex-direction: column;
  flex-wrap: nowrap;
}

.paper__main > ul {
  flex-direction: column;
}

</style>
