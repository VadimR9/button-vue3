<script setup>
import Button from "@/components/Button.vue";
import { ref } from "vue";

const disabled = ref(false);
const counter = ref();

const startTimer = (time) => {
  disabled.value = true;
  countDownTimer(time);
};

const timerOn = (time) => {
  counter.value = time;
  startTimer(time);
};

const countDownTimer = (time) => {
  if (time === 0) {
    disabled.value = false;
  }
  if (time > 0) {
    setTimeout(() => {
      counter.value = time -= 1;
      countDownTimer(time);
    }, 1000);
  }
};

const showAlert = () => {
  alert("Какое-то действие");
};
</script>

<template>
  <div class="custom">
    <div class="custom__item">
      <h2>Текстовая ссылка</h2>
      <div class="block">
        <p>UI</p>
        <Button label="Не помню пароль" link="https://www.google.com/" />
      </div>
    </div>

    <div class="custom__item">
      <h2>Кнопка</h2>

      <div class="block">
        <p class="subtitle">UI</p>
        <Button
          label="Отправить сообщение"
          color="primary"
          @click="showAlert"
        />
      </div>

      <div class="block">
        <p class="subtitle">Нерабочая (Disabled)</p>
        <Button label="Отправить сообщение" color="primary" disabled />
      </div>

      <div class="block">
        <p class="subtitle">С таймером</p>
        <Button
          v-if="!disabled"
          @timer-on="timerOn(60)"
          label="Отправить письмо"
          color="primary"
        />

        <Button
          v-else
          label="Повторное повторно"
          color="secondary"
          :timer="counter"
          disabled
        />
      </div>
    </div>

    <div class="custom__item">
      <h2>Кнопка с иконкой</h2>
      <p class="subtitle">UI</p>
      <div class="buttons">
        <div class="buttons__item">
          <Button
            color="primary"
            icon="close"
            size="small"
            @click="showAlert"
          />
          <Button color="primary" icon="close" @click="showAlert" />
        </div>
        <div class="buttons__item">
          <Button color="primary" icon="left" size="small" @click="showAlert" />
          <Button color="primary" icon="left" @click="showAlert" />
        </div>
        <div class="buttons__item">
          <Button
            color="primary"
            icon="right"
            size="small"
            @click="showAlert"
          />
          <Button color="primary" icon="right" @click="showAlert" />
        </div>
        <div class="buttons__item">
          <Button
            color="primary"
            icon="heart"
            size="small"
            @click="showAlert"
          />
          <Button color="primary" icon="heart" @click="showAlert" />
        </div>
      </div>
    </div>
    <div class="custom__item">
      <h2>Кнопка с иконкой справа</h2>
      <div class="block">
        <p class="subtitle">UI</p>
        <Button
          label="Отправить сообщение"
          color="primary"
          icon-right="right"
          @click="showAlert"
        />
      </div>

      <div class="block">
        <p class="subtitle">Нерабочая (Disabled)</p>
        <Button
          label="Отправить сообщение"
          color="primary"
          icon-right="right"
          disabled
        />
      </div>
    </div>
    <div class="custom__item">
      <h2>Кнопка с иконкой слева</h2>

      <div class="block">
        <p class="subtitle">UI</p>
        <Button
          label="Отправить сообщение"
          color="primary"
          icon-left="left"
          @click="showAlert"
        />
      </div>

      <div class="block">
        <p class="subtitle">Нерабочая (Disabled)</p>
        <Button
          label="Отправить сообщение"
          color="primary"
          icon-left="left"
          disabled
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "./styles/main.scss";
</style>
