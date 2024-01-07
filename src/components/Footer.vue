<script setup>
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits(['toggleFilter', 'clearAllCompleted']);

const { total, filter } = defineProps(['total', 'filter']);

const filterOptions = ['all', 'active', 'completed'];
</script>

<template>
  <footer class="footer">
    <div class="footer__top">
      <p class="footer__total">{{ total }} items lefts</p>
      <ul class="footer__filter">
        <li
          v-for="option in filterOptions"
          @click="emit('toggleFilter', option)"
          class="footer__filter__item"
          :class="{ active: filter === option }"
        >
          {{ option }}
        </li>
      </ul>
      <p @click="emit('clearAllCompleted')" class="footer__clear">
        Clear Completed
      </p>
    </div>
    <div class="footer__bottom">
      <ul class="footer__filter">
        <li
          v-for="option in filterOptions"
          @click="emit('toggleFilter', option)"
          class="footer__filter__item"
          :class="{ active: filter === option }"
        >
          {{ option }}
        </li>
      </ul>
    </div>
  </footer>
</template>

<style scoped>
.footer__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px 20px;
  background: var(--bg-secondary-color);
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
}

.footer__total,
.footer__filter__item,
.footer__clear {
  font-size: 14px;
  line-height: normal;
  letter-spacing: -0.194px;
  color: var(--text-secondary-color);
}

.footer__clear:hover,
.footer__filter__item:hover {
  color: var(--text-hover-color);
}

.footer__clear,
.footer__filter__item {
  cursor: pointer;
}
.footer__filter {
  display: flex;
  gap: 19px;
}

.footer__filter__item {
  text-transform: capitalize;
  font-weight: 700;
}

.footer__filter__item.active {
  color: var(--text-blue-color);
}

.footer__bottom {
  display: none;
}

@media (max-width: 768px) {
  .footer__top {
    padding: 16px 22px 20px;
  }

  .footer__top .footer__filter {
    display: none;
  }

  .footer__total,
  .footer__clear {
    font-size: 12px;
    letter-spacing: -0.167px;
  }

  .footer__bottom {
    display: flex;
    justify-content: center;
    padding: 16px;
    margin-top: 16px;
    background: var(--bg-secondary-color);
    border-radius: 5px;
  }

  .footer__filter__item {
    font-size: 14px;
    letter-spacing: -0.194px;
  }
}
</style>
