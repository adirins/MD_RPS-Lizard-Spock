<template>
  <div v-if="rules" class="wrapper">
      <div class="rules" @click="rules=false"></div>
  </div>
  <div v-else class="wrapper">
    <div class="container">
      <Header :rounds="rounds" :yourScore="yourScore" :computerScore="computerScore"/>
      <div class="row middle-xs center-xs game-wrapper">
        <div class="col-xs-3">
          <div v-for="weapon in weapons" :key="weapon" @click="chosenWeapon(weapon)">
            <div :class="weapon" class="btn"></div>
          </div>
        </div>
        <div class="col-xs-3 top-xs">
          <div v-if="yourChoice.length">
            <div :class="yourChoice" class="btn-chosen"></div>
          </div>
          <div v-else>
            What will be your weapon?
          </div>
        </div>
        <div class="col-xs-3 center-xs middle-xs flex">
          <Fight
           @attacking="attacking()"
           :result="result"
           :fighting="fighting"
           :yourChoice="yourChoice"
           />
        </div>
        <div class="col-xs-3">
          <Sheldon :computerChoice="computerChoice"/>
        </div>
      </div>
      <div class="row center-xs middle-xs footer">
        <Footer @chicken="reset()" @rules="rules=true"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Header from './components/header.vue';
import Footer from './components/footer.vue';
import Sheldon from './components/sheldon.vue';
import Fight from './components/fight.vue';

const Component = defineComponent({
  components: {
    Header,
    Footer,
    Sheldon,
    Fight,
  },

  data() {
    return {
      weapons: ['rock', 'paper', 'scissors', 'lizard', 'spock'],
      yourChoice: '',
      computerChoice: '',
      result: '',
      yourScore: 0,
      computerScore: 0,
      rounds: 0,
      fighting: false,
      rules: false,
      i: 0,
    };
  },

  methods: {
    chosenWeapon(item: string) {
      this.yourChoice = item;
      this.computerChoice = '';
      this.result = '';
    },

    attacking() {
      this.fighting = true;
      this.battle();
    },

    battle() {
      const interval = setInterval(() => {
        if (this.i !== 10) {
          this.computerChoice = this.weapons[Math.floor(Math.random() * this.weapons.length)];
          this.i += 1;
          console.log('i', this.i);
        } else {
          clearInterval(interval);
          console.log('wtf');
          this.fighting = false;
          this.battling();
          this.i = 0;
        }
      }, 80);
    },

    // eslint-disable-next-line consistent-return
    battling() {
      this.computerChoice = this.weapons[Math.floor(Math.random() * this.weapons.length)];

      if (this.yourChoice === this.computerChoice) {
        return this.draw();
      }

      if (this.yourChoice === 'rock') {
        if (this.computerChoice === 'lizard') {
          return this.win();
        }
        if (this.computerChoice === 'scissors') {
          return this.win();
        }
        if (this.computerChoice === 'spock') {
          return this.lost();
        }
        if (this.computerChoice === 'paper') {
          return this.lost();
        }
      }

      if (this.yourChoice === 'paper') {
        if (this.computerChoice === 'spock') {
          return this.win();
        }
        if (this.computerChoice === 'rock') {
          return this.win();
        }
        if (this.computerChoice === 'lizard') {
          return this.lost();
        }
        if (this.computerChoice === 'scissors') {
          return this.lost();
        }
      }

      if (this.yourChoice === 'scissors') {
        if (this.computerChoice === 'lizard') {
          return this.win();
        }
        if (this.computerChoice === 'paper') {
          return this.win();
        }
        if (this.computerChoice === 'rock') {
          return this.lost();
        }
        if (this.computerChoice === 'spock') {
          return this.lost();
        }
      }

      if (this.yourChoice === 'lizard') {
        if (this.computerChoice === 'spock') {
          return this.win();
        }
        if (this.computerChoice === 'paper') {
          return this.win();
        }
        if (this.computerChoice === 'rock') {
          return this.lost();
        }
        if (this.computerChoice === 'scissors') {
          return this.lost();
        }
      }

      if (this.yourChoice === 'spock') {
        if (this.computerChoice === 'scissors') {
          return this.win();
        }
        if (this.computerChoice === 'rock') {
          return this.win();
        }
        if (this.computerChoice === 'lizard') {
          return this.lost();
        }
        if (this.computerChoice === 'paper') {
          return this.lost();
        }
      }
    },

    draw() {
      this.result = 'It is a draw!';
      this.rounds += 1;
    },

    win() {
      this.result = 'You won!';
      this.rounds += 1;
      this.yourScore += 1;
    },

    lost() {
      this.result = 'You lost!';
      this.rounds += 1;
      this.computerScore += 1;
    },
    reset() {
      this.yourChoice = '';
      this.computerChoice = '';
      this.result = '';
      this.yourScore = 0;
      this.computerScore = 0;
      this.rounds = 0;
    },
  },
});
export default Component;
</script>

<style lang="scss" >
@import './App.scss';
</style>
