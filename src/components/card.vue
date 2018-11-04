<template>
  <div class="card-field" :class="{ 'clear-card': isCleared, 'card-front': isFront }"  @click="openCard">
    <div v-if="isFront">
      <div v-if="number !== 0" class="card active-card">
        {{ number }}
      </div>
      <div v-else class="card clear-card"></div>
    </div>
    <div v-else>
      <div v-if="!isCleared" class="card card-back">俺</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    number: {
      type: Number,
      required:true
    },
  },
  data () {
    return {
      isFront: true
    }
  },
  computed: {
    isCleared() {
      return this.number === 0;
    }
  },
  methods: {
    openCard() {
      if (this.isFront) return;
      this.isFront = true;
      this.$emit('setCardPair', this.number)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.card-field {
  display: inline-block;
  width: 40px;
  height: 50px;
  margin: 5px;
  position: relative;
  border: 4px double #666;
  border-radius: 3px;
}

.card {
  position: absolute;
  line-height: 50px;
  top: 0px;
  left: 0px;
  right: 0px;
  bottom: 0px;
}

.active-card {
  cursor: default;
}

.card-back {
  box-sizing: border-box;
  cursor: pointer;
  margin: 0 auto;
  line-height: 45px;
}

.card-front {
  border: 1px double #666;
}

.clear-card {
  border: none;
}
</style>
