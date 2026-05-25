<script setup>
import { ref } from 'vue'
import './styles/common.css'
import './styles/themes.css'

const data = [
  { icon: 'fa-user', text: 'People' },
  { icon: 'fa-star', text: 'Favourites' },
  { icon: 'fa-check-square', text: 'Todos' },
  { icon: 'fa-compass', text: 'Explore' },
  null,
  { icon: 'fa-image', text: 'Images' },
  { icon: 'fa-bell', text: 'Notification' }
]

const themes = ['light', 'dark', 'red']
const currentTheme = ref(themes[0])
const toggleTheme = () => {
  let index = themes.indexOf(currentTheme.value)
  index = (index + 1) % themes.length
  currentTheme.value = themes[index]
}

const activeIndex = ref(-1)
const itemClick = index => {
  if (index === 4) return
  activeIndex.value = index
}
</script>

<template>
  <div class="container" :class="currentTheme">
    <i class="logo fab fa-fw fa-apple" @click="toggleTheme"></i>
    <div class="input-group">
      <i class="icon fas fa-fw fa-search"></i>
      <input type="search" class="search" placeholder="Search" />
    </div>
    <ul class="menu">
      <li
        v-for="(item, index) in data"
        :class="[
          data[index] ? 'menu-item' : 'divider',
          { active: activeIndex === index }
        ]"
        @click="itemClick(index)"
      >
        <template v-if="item">
          <i class="icon fas fa-fw" :class="item.icon"></i>
          {{ `${item.text}` }}
        </template>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 2rem;
  color: var(--text-color);
  background: var(--bg-color);
  border-radius: 10px;
  box-shadow: 0 0 20px var(--shadow-color);
  user-select: none;

  .logo {
    align-self: center;
    margin-bottom: 1.5rem;
    color: var(--logo-color);
    font-size: 1.8rem;
    cursor: pointer;
  }

  .icon {
    margin-right: 1.2rem;
    font-size: 1.1rem;
  }

  .input-group {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
    padding: 0.75rem 1rem;
    color: var(--input-color);
    background: var(--input-bg-color);
    border-radius: 8px;

    .search {
      margin: 0;
      padding: 0;
      width: 100%;
      color: var(--input-color);
      outline: none;
      border: none;
      background: transparent;

      &::placeholder {
        color: var(--input-color);
      }
    }
  }

  .menu {
    display: flex;
    flex-direction: column;
    width: 240px;

    .menu-item {
      display: flex;
      align-items: center;
      margin-top: 0.5rem;
      padding: 0.75rem 1rem;
      cursor: pointer;
      transition: 0.3s;

      &.active {
        color: var(--active-color);
        background: var(--active-bg-color);
        border-radius: 8px;
      }
    }

    .divider {
      align-self: center;
      width: 126%;
      height: 2px;
      margin: 1rem 0;
      background: var(--divider-color);
    }
  }
}
</style>
