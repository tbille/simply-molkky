<template>
  <div class="score-selector">
    <div class="pins">
      <Pin
        v-for="number in 12"
        :key="number"
        @pinClicked="onPinClick"
        :isSelected="selected.includes(number)"
        :number="number"/>
    </div>
    <button class="btn btn-validate" @click="validateScore" v-html="$t(okMessage, { score })">{{okMessage}}</button>
  </div>
</template>


<script>
import Pin from './Pin';

export default {
  components: {
    Pin,
  },
  data() {
    return {
      selected: [],
    };
  },
  computed: {
    score() {
      if (this.selected.length === 1) {
        return this.selected[0];
      }

      return this.selected.length;
    },
    okMessage() {
      return this.score > 0
        ? 'game.submit.ok'
        : 'game.submit.missed';
    },
  },
  methods: {
    onPinClick(number) {
      const index = this.selected.indexOf(number);
      if (index > -1) {
        this.selected.splice(index, 1);
      } else {
        this.selected.push(number);
      }
    },
    resetScore() {
      this.selected = [];
    },
    validateScore() {
      this.$emit('validateScore', this.score);
      this.resetScore();
    },
  },
};
</script>

<style lang="less" scoped>
@import "../../style/variables";
.score-selector {
  width: 100%;
}

.pins {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(1rem, 1fr));
  grid-gap: .5rem;
  max-width: 80%;
  margin: auto;

  .🎳 {
    margin-top: -15%;
    width: auto;
    grid-column-end: span 2;
    grid-row-end: span 2;

    &:nth-child(7),
    &:nth-child(9),
    &:nth-child(8) {
      grid-row-start: 1;
    }
    &:nth-child(7) {
      grid-column-start: 2;
    }
    &:nth-child(9) {
      grid-column-start: 4;
    }
    &:nth-child(8) {
      grid-column-start: 6;
    }

    &:nth-child(5),
    &:nth-child(11),
    &:nth-child(12),
    &:nth-child(6) {
      grid-row-start: 3;
    }
    &:nth-child(5) {
      grid-column-start: 1;
    }
    &:nth-child(11) {
      grid-column-start: 3;
    }
    &:nth-child(12) {
      grid-column-start: 5;
    }
    &:nth-child(6) {
      grid-column-start: 7;
    }

    &:nth-child(3),
    &:nth-child(10),
    &:nth-child(4) {
      grid-row-start: 5;
    }
    &:nth-child(3) {
      grid-column-start: 2;
    }
    &:nth-child(10) {
      grid-column-start: 4;
    }
    &:nth-child(4) {
      grid-column-start: 6;
    }

    &:nth-child(1),
    &:nth-child(2) {
      grid-row-start: 7;
    }
    &:nth-child(1) {
      grid-column-start: 3;
    }
    &:nth-child(2) {
      grid-column-start: 5;
    }
  }
}

button {
  margin-top: 1.5rem;
}
</style>
