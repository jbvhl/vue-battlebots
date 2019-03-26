<template>
  <div id="app">
    <div id="nav">
      <button @click="toggle(true)">Create</button>
      <h1>Battle Bots</h1>
      <button @click='toggle(false)'>Collection</button>
      <section v-if="showForm">
        <input placeholder="Bot Name*" v-model="bot">
        <input placeholder="Attack Value*" v-model="attack">
        <input placeholder="HealthValue*" v-model="health">
        <button @click="addBot">Submit</button>
        <button @click="clearBot">Clear</button>
      </section>
      <section v-else>
        <h2 v-if="selectedBots[0]">Bot #1: {{selectedBots[0].bot}}</h2>
        <h2 v-else>Bot #1: Select a bot below</h2>
        <h2 v-if="selectedBots[1]">Bot #2: {{selectedBots[1].bot}}</h2>
        <h2 v-else>Bot #2: Select a bot below</h2>
        <button @click='battle'>Battle</button>
        <button @click='clearSelected'>Clear</button>
        <bot v-for='(botObj, i) in allBots' :key='i' :index='i' :botObj='botObj' :deleteBot='deleteBot' :selectBot='selectBot'/>
      </section>
    </div>
  </div>
</template>

<script>
import Bot from './components/Bot';

export default {
  name: "app",
  data() {
    return {
      showForm: true,
      bot: "",
      attack: 0,
      health: 0,
      allBots: [],
      selectedBots: []
    };
  },

  methods: {
    toggle(val) {
      this.showForm = val;
    },

    addBot() {
      const newBot = {
        bot: this.bot,
        attack: this.attack,
        health: this.health
      };
      this.allBots.push(newBot);
      this.bot = "";
      this.attack = 0;
      this.health = 0;
      this.toggle();
    },
    clearBot() {
      this.bot = "";
      this.attack = 0;
      this.health = 0;
    },

    clearSelected() {
      this.selectedBots = [];
    },

    deleteBot(i) {
      this.allBots.splice(i, 1)
    },

    selectBot(botObj) {
      if (this.selectedBots.length < 2) {
        this.selectedBots.push(botObj)
      } else {
        alert('2 bots already selected');
      }
    },

    battle() {
      if (this.selectedBots[0].attack > this.selectedBots[1].attack) {
        alert(`${this.selectedBots[0].bot} wins!`);
      } else {
        alert(`${this.selectedBots[1].bot} wins!`);
      }
      this.selectedBots = [];
    }
  },
  components: {
    Bot
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
