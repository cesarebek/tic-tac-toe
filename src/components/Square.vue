<template>
  <button
    class="square"
    :class="[value, { winner: winner }]"
    :disabled="disabled"
    @click="click"
  >
    {{ value }}
  </button>
</template>

<script>
export default {
  name: 'Square',
  props: {
    value: String,
    winner: Boolean,
    disabled: Boolean,
  },
  methods: {
    click() {
      this.$emit('click');
    },
  },
};
</script>

<style scoped>
.square {
  cursor: pointer;
  background: #fff9;
  border: 1px solid #fffc;
  font-size: 15vmin;
  font-weight: bold;
  line-height: 34px;
  padding: 0;
  text-align: center;
  text-shadow: -1px -1px 1px #000b, -1px 1px 1px #000b, 1px -1px 1px #000b,
    1px 1px 1px #000b;
  transition: all 0.25s ease;
}

.square.winner {
  background: #8885;
}

.square:not([disabled]):empty:active {
  box-shadow: inset 0 2px 50px #0008;
}

.square.X {
  color: lightcoral;
}

.square.O {
  color: lightskyblue;
}
</style>
