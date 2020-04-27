<template>
  <div class="deal">
    <h1>May the Odds be Ever in Your Favor</h1>
    <div id="selectors">
      <div id="row">
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
      <br />
      <div id="row">
        <label>Cards</label>
        <input type="radio" id="numCards" value="5" v-model="size" />
        <label for="one">Five</label>
        <input type="radio" id="numCards" value="6" v-model="size" />
        <label for="one">Six</label>
        <input type="radio" id="numCards" value="7" v-model="size" />
        <label for="two">Seven</label>
        <input type="radio" id="numCards" value="8" v-model="size" />
        <label for="two">Eight</label>
        <input type="radio" id="numCards" value="9" v-model="size" />
        <label for="two">Nine</label>
      </div>
    </div>
    <div id="playerButtons">
      <button
        class="playerButton"
        id="player1"
        v-if="players > 0 && dealt == true"
        v-on:click="setPlayer(1)"
      >Player 1</button>
      <button
        class="playerButton"
        id="player2"
        v-if="players > 1 && dealt == true"
        v-on:click="setPlayer(2)"
      >Player 2</button>
      <button
        class="playerButton"
        id="player3"
        v-if="players > 2 && dealt == true"
        v-on:click="setPlayer(3)"
      >Player 3</button>
      <button
        class="playerButton"
        id="player4"
        v-if="players > 3 && dealt == true"
        v-on:click="setPlayer(4)"
      >Player 4</button>
    </div>
    <div id="cards">
      <div
        v-for="(card, index) in hands[show_player - 1]"
        :key="index"
        style="display: inline-block"
      >
        <span style="display: block">
          <img v-if="!dealt" id="playingCard" src="../assets/cards/dkelion.jpg" alt="card" />
          <img v-if="dealt" id="playingCard" :src="getImgUrl(card)" alt="card" />
          <input
            v-if="dealt && show_player !== 5"
            type="checkbox"
            value="true"
            style="display: block; margin-left: 70px"
            v-model="wantNew[show_player - 1][index]"
          />
        </span>
      </div>
      <!-- <div id="discardBox" style="display: block">
        <div v-for="(discard, index) in wantNew[show_player - 1]" style="display: inline-block">
          <input v-if="dealt && show_player !== 5" type="checkbox" value="true" />
        </div>
      </div>-->
    </div>
    <!-- <div style="display: inine-block"> -->
    <button
      class="cardButton"
      id="dealButton"
      v-on:click="deal"
      @mouseover="hover = true"
      @mouseleave="hover = false"
    >Deal Cards</button>
    <button
      v-if="dealt && show_player != 5"
      class="cardButton"
      id="discardButton"
      v-on:click="discard"
      @mouseover="hover = true"
      @mouseleave="hover = false"
    >Discard Selected</button>
    <!-- </div> -->
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      hands: [],
      wantNew: [[], [], [], []],
      remainderDeck: [],
      players: 1,
      dealt: false,
      size: 5,
      show_player: 5,
      card: "",
      default_url: "../assets/logo.png",
      test: "logo",
      hover: false
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
      [],
      [
        "dkelion.jpg",
        "dkelion.jpg",
        "dkelion.jpg",
        "dkelion.jpg",
        "dkelion.jpg"
      ]
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
      this.show_player = 5;
      this.hands = [
        [],
        [],
        [],
        [],
        [
          "dkelion.jpg",
          "dkelion.jpg",
          "dkelion.jpg",
          "dkelion.jpg",
          "dkelion.jpg"
        ]
      ];
      this.dealt = true;
      for (let x = 0; x < this.size; x++) {
        for (let y = 0; y < this.players; y++) {
          let dealt = Math.floor(Math.random() * deck.length);
          let card_url = deck[dealt] + ".png";
          // this.hands[y].splice(x, 1, card_url);
          this.hands[y].push(card_url);
          deck.splice(dealt, 1);
          this.wantNew[y].push(false);
        }
      }
      this.remainderDeck = [...deck];
    },
    discard() {
      this.wantNew[this.show_player - 1].forEach((card, index) => {
        if (card) {
          let newCard =
            this.remainderDeck.splice(
              Math.floor(Math.random() * this.remainderDeck.length),
              1
            ) + ".png";
          this.hands[this.show_player - 1].splice(index, 1, newCard);
          this.wantNew[this.show_player - 1][index] = false;
        }
      });
      console.log(this.remainderDeck.length);
    },
    getImgUrl(card) {
      return require("../assets/cards/" + card);
    },
    setPlayer(player) {
      this.show_player = player;
    }
  }
};
</script>

<style scoped>
#selectors {
  padding-bottom: 20px;
}

#row {
  display: inline-block;
  padding-bottom: 10px;
}

#players {
  margin-left: 25px;
}

#numCards {
  margin-left: 25px;
}

#cards {
  margin-bottom: 30px;
}

#playingCard {
  height: 150px;
}

.cardButton {
  width: 200px;
  height: 60px;
  background-color: whitesmoke;
  color: #000;
  font-weight: bold;
  border-style: solid;
  border-width: 3px;
  font-size: 20px;
}
#dealButton {
  margin-right: 20px;
}

#dealButton:hover {
  background-color: navy;
  color: white;
}

#discardButton {
  margin-left: 20px;
}

#discardButton:hover {
  background-color: red;
  color: white;
}

.playerButton {
  width: 100px;
  height: 50px;
  border-style: solid;
  border-width: 2px;
  border-color: #000;
  margin: 15px;
  color: white;
  font-weight: bolder;
  font-size: 18px;
}
#player1 {
  background-color: blue;
}

#player2 {
  background-color: red;
}

#player3 {
  background-color: black;
}

#player4 {
  background-color: darkgreen;
}
</style>