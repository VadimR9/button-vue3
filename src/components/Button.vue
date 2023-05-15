<template>
  <a v-if="link" class="btn btn_link" :href="link">{{ label }}</a>
  <button
    v-else
    :class="[
      'btn',
      `btn_${color}`,
      { btn_rounded: rounded },
      { btn_icon: icon },
      { btn_small: size === 'small' },
    ]"
    :disabled="disabled"
    @click="clickOnButton(), timerOn()"
  >
    <span v-if="icon">
      <i :class="`icon-${icon}`"></i>
    </span>

    <span v-else-if="timer">
      {{ label }} <b>{{ secondsToTime(timer) }}</b>
    </span>
    <span v-else>
      <i v-if="iconLeft" :class="`left icon-${iconLeft}`"></i>
      {{ label }}
      <i v-if="iconRight" :class="`right icon-${iconRight}`"></i>
    </span>
  </button>
</template>

<script setup>
const props = defineProps({
  label: {
    type: String,
    default: "Button",
  },
  color: {
    type: String,
    default: "primary",
  },
  disabled: {
    type: Boolean,
    required: false,
  },
  rounded: {
    type: Boolean,
    required: false,
  },
  icon: {
    type: String,
    required: false,
  },
  iconLeft: {
    type: String,
    required: false,
  },
  iconRight: {
    type: String,
    required: false,
  },
  size: {
    type: String,
    default: "normal",
  },
  timer: {
    type: Number,
    required: false,
  },
  link: {
    type: String,
    required: false,
  },
});

const emit = defineEmits(["click", "timer-on"]);
const clickOnButton = () => {
  emit("click");
};
const timerOn = () => {
  emit("timer-on");
};

const secondsToTime = (counter) => {
  counter = Number(counter);
  const h = Math.floor(counter / 3600);
  const m = Math.floor((counter % 3600) / 60);
  const s = Math.floor((counter % 3600) % 60);
  const hDisplay = h > 0 ? `${(h < 10 ? 0 : "") + h}:` : "";
  const mDisplay = m > 0 ? `${m}:` : "0:";
  const sDisplay = (s < 10 ? "0" : "") + s;
  return hDisplay + mDisplay + sDisplay;
};
</script>

<style lang="scss" scoped>
@import "@/styles/ui/button.scss";
</style>
