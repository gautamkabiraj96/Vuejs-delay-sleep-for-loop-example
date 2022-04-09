<template>
  <div id="app">
    <div
      @click="playQuote()"
      class="np-play-button"
      :class="{
        'np-play-button-black': isQuotePlaying,
        'np-play-button-white': !isQuotePlaying,
      }"
    >
      Play
    </div>
    <div>
      <div class="np-quote-text">
        <span>{{ quoteToDisplayString }}</span>
        <span v-show="showBlinking">|</span>
      </div>
    </div>
    <!-- www.nightprogrammer.com -->
  </div>
</template>

<script>
export default {
  name: "Quote",
  data() {
    return {
      quoteToDisplay: [],
      quoteToDisplayString: "",
      quoteString: `Die with memories, not dreams.`,
      quotesList: [],
      isQuotePlaying: false,
      quoteTypingAnimationDelay: 100,
      fontSize: 40,
      showBlinking: false,
      blinkingAnimationDelay: 300,
    };
  },
  mounted() {
    setInterval(() => {
      this.showBlinking = !this.showBlinking;
    }, this.blinkingAnimationDelay);
  },
  methods: {
    sleep(milliseconds) {
      return new Promise((resolve) => setTimeout(resolve, milliseconds));
    },
    async playQuote() {
      if (this.isQuotePlaying) return;

      this.quoteToDisplay = [];
      this.quoteToDisplayString = "";
      this.quotesList = this.quoteString.split("");
      this.isQuotePlaying = true;
      for (let i = 0; i < this.quotesList.length; i++) {
        await this.sleep(this.quoteTypingAnimationDelay);
        this.quoteToDisplay.push(this.quotesList[i]);
        this.quoteToDisplayString = this.quoteToDisplay.join("");
        if (i === this.quotesList.length - 1) this.isQuotePlaying = false;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body {
  background-color: rgb(24, 24, 24);
  padding: 30px;
}
.np-play-button {
  color: #fff;
  padding-bottom: 30px;
  cursor: pointer;
  width: 200px;
  height: 20px;
}
.np-play-button-white {
  color: #fff;
}
.np-play-button-black {
  color: rgb(24, 24, 24);
}
.np-quote-text {
  font-size: 40px;
  font-weight: bold;
  line-height: 1.2;
  color: #fff;
  font-style: italic;
}
</style>
