<script setup>
import { ref, watch, onMounted } from 'vue';

import Input from './components/Input.vue';
import Nav from './components/Nav.vue';
import Item from './components/Item.vue';
import Footer from './components/Footer.vue';

const list = ref([]);
const filter = ref('all');
const total = ref(list.value.length);
const theme = ref('dark');

onMounted(() => {
  window.addEventListener('resize', () => getImageSrc());

  const localList = localStorage.getItem('todoAppList')
    ? JSON.parse(localStorage.getItem('todoAppList'))
    : [];

  if (localList.length) {
    list.value = localList;
  }
});

const addTodo = (value) => {
  list.value.push({ id: Math.random() * 10000, text: value, completed: false });

  localStorage.setItem('todoAppList', JSON.stringify(list.value));
};

const deleteTodo = (id) => {
  list.value = list.value.filter((item) => item.id !== id);

  localStorage.setItem('todoAppList', JSON.stringify(list.value));
};

const toggleCompletion = (id) => {
  const item = list.value.find((item) => item.id === id);

  item.completed = !item.completed;

  localStorage.setItem('todoAppList', JSON.stringify(list.value));
};

const clearAllCompleted = () => {
  list.value = list.value.filter((item) => item.completed === false);

  localStorage.setItem('todoAppList', JSON.stringify(list.value));
};

const toggleFilter = (value) => {
  filter.value = value;
};

const toggleTheme = () => {
  if (theme.value === 'dark') {
    theme.value = 'light';
    document.documentElement.classList.add('light');
  } else {
    theme.value = 'dark';
    document.documentElement.classList.remove('light');
  }
};

const getImageSrc = () => {
  if (window.innerWidth > 768) {
    return `/bg-desktop-${theme.value}.jpeg`;
  } else {
    return `/bg-mobile-${theme.value}.jpeg`;
  }
};

watch(filter, () => {
  if (filter.value === 'all') {
    total.value = list.value.length;
  } else if (filter.value === 'active') {
    total.value = list.value.filter((item) => item.completed === false).length;
  } else {
    total.value = list.value.filter((item) => item.completed === true).length;
  }
});
</script>

<template>
  <img class="background__img" :src="getImageSrc()" alt="" />
  <div class="container">
    <Nav :theme="theme" @toggleTheme="toggleTheme" />
    <Input @addTodo="addTodo" />
    <section>
      <Item
        v-if="filter === 'all'"
        v-for="item in list"
        :key="`all-${item.id}`"
        :item="item"
        @deleteTodo="deleteTodo"
        @toggleCompletion="toggleCompletion"
      />
      <Item
        v-else-if="filter === 'active'"
        v-for="item in list.filter((item) => item.completed === false)"
        :key="`active-${item.id}`"
        :item="item"
        @deleteTodo="deleteTodo"
        @toggleCompletion="toggleCompletion"
      />
      <Item
        v-else
        v-for="item in list.filter((item) => item.completed === true)"
        :item="item"
        :key="`completed-${item.id}`"
        @deleteTodo="deleteTodo"
        @toggleCompletion="toggleCompletion"
      />
    </section>
    <Footer
      @toggleFilter="toggleFilter"
      @clearAllCompleted="clearAllCompleted"
      :total="total"
      :filter="filter"
    />
  </div>
</template>

<style scoped>
.container {
  max-width: 540px;
  margin: 0 auto;
}

section {
  margin-top: 24px;
  background: var(--bg-secondary-color);
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  box-shadow: 0px 35px 50px -15px rgba(0, 0, 0, 0.5);
}

.background__img {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 300px;
  z-index: -1;
  object-fit: cover;
}

@media (max-width: 768px) {
  .container {
    max-width: none;

    padding: 0 24px;
  }
}
</style>
