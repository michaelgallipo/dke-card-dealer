<template>
  <div class="deal">
    <h1>May the Odds be Ever in Your Favor</h1>
    <div id="cards">
      <div v-for="card in hands[0]" style="display: inline-block">
        <span>
          <img id="playingCard" :src="getImgUrl(card)" alt="card" />
        </span>
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
      hand1: [],
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
    this.hand1 = [
      "dkelion.jpg",
      "dkelion.jpg",
      "dkelion.jpg",
      "dkelion.jpg",
      "dkelion.jpg"
    ];
    console.log("created worked", this.hands);
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
      for (let x = 0; x < size; x++) {
        let dealt = Math.floor(Math.random() * deck.length);
        let card_url = deck[dealt] + ".png";
        this.hands[0].splice(x, 1, card_url);
        deck.splice(dealt, 1);
        // console.log(this.hands[0]);
      }
    },
    getImgUrl(card) {
      return require("../assets/cards/" + card);
    }
  }
};
</script>

<style scoped>
#cards {
  margin-bottom: 30px;
}
#playingCard {
  height: 150px;
}
</style>