<template>
  <div class="deal">
    <h1>May the Odds be Ever in Your Favor</h1>
    <div id="selectors">
      <label>Players</label>
      <input type="radio" id="players" value="1" v-model="players" />
      <label for="one">One</label>
      <input type="radio" id="players" value="2" v-model="players" />
      <label for="two">Two</label>
      <input type="radio" id="players" value="3" v-model="players" />
      <label for="three">Three</label>
      <input type="radio" id="players" value="4" v-model="players" />
      <label for="four">Four</label>
    </div>
    <div id="cards">
      <div v-for="(player, index) in hands" :key="index">
        <div v-if="index < players">
          <div v-for="(card, index) in player" :key="index" style="display: inline-block">
            <span>
              <img id="playingCard" :src="getImgUrl(card)" alt="card" />
            </span>
          </div>
        </div>
      </div>
    </div>
    <button v-on:click="deal">Deal Cards</button>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      hands: [],
      players: 1,
      card: "",
      default_url: "../assets/logo.png",
      test: "logo"
    };
  },
  created() {
    this.hands = [
      [
        "dkelion.jpg",
        "dkelion.jpg",
        "dkelion.jpg",
        "dkelion.jpg",
        "dkelion.jpg"
      ],
      [],
      [],
      []
    ];
  },
  methods: {
    deal: function() {
      const deck = [
        "2C",
        "3C",
        "4C",
        "5C",
        "6C",
        "7C",
        "8C",
        "9C",
        "10C",
        "JC",
        "QC",
        "KC",
        "AC",
        "2S",
        "3S",
        "4S",
        "5S",
        "6S",
        "7S",
        "8S",
        "9S",
        "10S",
        "JS",
        "QS",
        "KS",
        "AS",
        "2D",
        "3D",
        "4D",
        "5D",
        "6D",
        "7D",
        "8D",
        "9D",
        "10D",
        "JD",
        "QD",
        "KD",
        "AD",
        "2H",
        "3H",
        "4H",
        "5H",
        "6H",
        "7H",
        "8H",
        "9H",
        "10H",
        "JH",
        "QH",
        "KH",
        "AH"
      ];
      let size = 5;
      this.hands = [[], [], [], []];
      for (let x = 0; x < size; x++) {
        for (let y = 0; y < this.players; y++) {
          let dealt = Math.floor(Math.random() * deck.length);
          let card_url = deck[dealt] + ".png";
          // this.hands[y].splice(x, 1, card_url);
          this.hands[y].push(card_url);
          deck.splice(dealt, 1);
        }
      }
    },
    getImgUrl(card) {
      return require("../assets/cards/" + card);
    }
  }
};
</script>

<style scoped>
#selectors {
  display: inline-block;
  padding-bottom: 30px;
}

#players {
  margin-left: 25px;
}

#cards {
  margin-bottom: 30px;
}

#playingCard {
  height: 150px;
}
</style>