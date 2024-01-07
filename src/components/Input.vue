<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits(['addTodo']);

const input = ref('');

const onInputSubmit = (e) => {
  e.preventDefault();

  emit('addTodo', input.value);

  input.value = '';
};
</script>

<template>
  <div class="input">
    <svg
      class="input__icon"
      xmlns="http://www.w3.org/2000/svg"
      width="100%"
      height="100%"
      viewBox="0 0 25 24"
      fill="none"
    >
      <circle cx="12" cy="12" r="12" stroke="#393A4B" />
    </svg>
    <form class="input__form" @submit="onInputSubmit">
      <input
        @submit="onInputSubmit()"
        v-model="input"
        class="input__form__text"
        type="text"
        placeholder="Create a new todo…"
      />
    </form>
  </div>
</template>

<style scoped>
.input {
  width: 100%;
  padding: 20px 24px;
  display: flex;
  align-items: center;
  gap: 24px;
  background: var(--bg-secondary-color);
  border-radius: 5px;
  box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
}

.input__icon {
  width: 24px;
  height: 24px;
}

.input__icon circle {
  stroke: var(--text-border-color);
}

.input__form {
  width: 100%;
  height: 100%;
}

.input__form__text {
  width: 100%;
  border: none;
  background: transparent;
  color: var(--text-primary-color);
  font-family: 'Josefin Sans', sans-serif;
  font-size: 18px;
  letter-spacing: -0.25px;
}

.input__form__text::placeholder {
  color: var(--text-placeholder-color);
  font-family: 'Josefin Sans', sans-serif;
  font-size: 18px;
  letter-spacing: -0.25px;
}

.input__form__text:focus {
  outline: navajowhite;
}

@media (max-width: 768px) {
  .input {
    gap: 12px;
  }

  .input__icon {
    width: 20px;
    height: 20px;
  }

  .input__form__text {
    font-size: 12px;
    letter-spacing: -0.167px;
  }

  .input__form__text::placeholder {
    font-size: 12px;
    letter-spacing: -0.167px;
  }
}
</style>
