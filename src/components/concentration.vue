<template>
  <div class="contents-field">
    <img src="../assets/title-logo.png" class="title">
    <div v-if="gameCleared" class="clear-message">
      <p>おめでとう！貴方こそ真の<img src="../assets/ore.png"></p>
      <p>である!</p>
    </div>
    <div class="cards-field">
      <transition-group name="cards" tag="div" class="container">
        <card-component v-for="card in cardSet"
          :key="card.id"
          :number="card.num"
          @setCardPair="setCard"
          ref="oneCard"
          :class="{ 'cannot-reverse': card_pair.length === 2 || beforeStart }"
        />
      </transition-group>
    </div>

    <div clas="start-menu" v-if="beforeStart">
      <div class="input-field">
        <p>プレイするカードの枚数を入力してください</p>
        <p>(1 ~ 50枚)</p>
        <input type="text" v-model.number="cardCount">
      </div>
      <div class="button-field">
        <button @click="gameStart" :class="{ 'cant-start': cardSet.length === 0 }">ゲームスタート</button>
      </div>
    </div>
  </div>
</template>

<script>
import CardComponent from './card'
export default {
  name: 'Concentration',
  components: {
    CardComponent
  },
  data () {
    return {
      msg: '',
      beforeStart: true,
      cardCount: '',
      cardSet: [],
      card_pair: [],
      gameCleared: false
    }
  },
  watch: {
    cardCount(num) {
      if (num < 0 || num > 50) return;
      this.cardSet = [];
      for(let i = 1; i <= num; i++) {
        this.cardSet.push({ id: (2 * i - 1), num: i });
        this.cardSet.push({ id: (2 * i), num: i});
      }
    }
  },
  methods: {
    setCard(num) {
      this.card_pair.push(num);
      if(this.card_pair.length === 2) {
        this.judgeCard();
      }
    },
    gameStart() {
      let i = 0;
      let shuffleId = 0;
      const startShuffle = () => {
        shuffleId = setInterval(shuffle, 700);
      };
      const stopShuffle = () => {
        clearInterval(shuffleId);
      };
      const shuffle = () => {
        this.shuffleCards();
        i++;
        if (i >= 3) {
          stopShuffle();
        }
      };
      this.$refs.oneCard.forEach(e => {
        e.isFront = false;
      });
      startShuffle();
      this.beforeStart = false;
    },
    shuffleCards() {
      this.cardSet = _.shuffle(this.cardSet);
    },
    judgeCard() {
      setTimeout(this.checkCardPair, 700)
    },
    checkCardPair() {
      if (this.card_pair[0]=== this.card_pair[1]) {
        this.cardSet.forEach((card, index) => {
          if (card.num === this.card_pair[1]) {
            card.num = 0;
          }
        });
        const isNoCards = this.cardSet.every(card => card.num === 0);
        if (isNoCards) {
          this.gameCleared = true;
        }
        this.card_pair = [];
      } else {
        this.$refs.oneCard.forEach(e => {
          e.isFront = false;
        });
        this.card_pair = [];
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.contents-field {
    max-width: 750px;
    margin: 0 auto;
}

.cards-field {
  min-height: 300px;
}

.cannot-reverse {
  pointer-events: none;
}

.cards-move {
  transition: all 1s;
}

input {
  border: 2px solid #999;
  font-size: 14px;
  height: 30px;
  border-radius: 3px;
}

.button-field {
  margin-bottom: 100px;
}

.button-field button{
  margin-top: 30px;
  height: 30px;
  border-radius: 5px;
  border: none;
  box-shadow: 0px 3px 10px rgba(0,0,0,0.4);
  background-color: #1e90ff;
  color: white;
  transition: all 0.5s;
  cursor: pointer;
}

button.cant-start {
  transition: all 0.5s;
  pointer-events: none;
  background-color: rgba(30, 144, 255, 0.4);
  box-shadow: none;
  cursor: default;
}

.clear-message {
  font-weight: bold;
  font-size: 36px;
}

.ore {
  font-size: 50px;
  color: #dc143c;
}

img {
  max-width: 100%;
}

img.title {
  margin-top: 50px;
}

</style>
