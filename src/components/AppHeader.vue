<script setup lang="ts">
import type { Page } from '@/interfaces'
import { ref } from 'vue'
import AppCalc from './AppCalc.vue'

const open = ref<boolean>(false)

defineProps<{
  page: Page
}>()

const emit = defineEmits<{
  (e: 'navigate', page: Page): void
}>()
</script>

<template>
  <header class="px-20 d-flex flex-row align-items-center">
    <a href="#" class="d-flex flex-row align-items-center mr-20">
      <img src="../assets/logo.svg" />
      <span class="logo">Dyma</span>
    </a>
    <div class="d-flex flex-row align-items-center flex-fill actions-container">
      <ul class="d-flex flex-row flex-fill hide-xs flex-fill">
        <li class="mr-10">
          <a :class="{ active: page === 'AppBoutique' }" @click="emit('navigate', 'AppBoutique')"
            >Boutique</a
          >
        </li>
        <li>
          <a :class="{ active: page === 'AppAdmin' }" @click="emit('navigate', 'AppAdmin')"
            >Admin</a
          >
        </li>
      </ul>
      <ul class="d-flex flex-row hide-xs">
        <li class="mr-10">
          <a href="#">Inscription</a>
        </li>
        <li>
          <a href="#">Connexion</a>
        </li>
      </ul>
      <div class="menu-xs-container">
        <AppCalc :open="open" @close="open = false" :transparent="true" />
        <i @click="open = !open" class="fa-solid fa-bars show-xs"></i>
        <Transition>
          <ul @click="open = false" v-if="open" class="menu card">
            <li>
              <a
                :class="{ active: page === 'AppBoutique' }"
                @click="emit('navigate', 'AppBoutique')"
                >Boutique</a
              >
            </li>
            <li>
              <a :class="{ active: page === 'AppAdmin' }" @click="emit('navigate', 'AppAdmin')"
                >Admin</a
              >
            </li>
            <li>
              <a href="#">Inscription</a>
            </li>
            <li>
              <a href="#">Connexion</a>
            </li>
          </ul>
        </Transition>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
@use '@/assets/scss/mixins';

header {
  background-color: var(--primary-1);
  a {
    color: var(--text-primary-color);
    img {
      width: 20px;
      margin-right: 5px;
    }
    .logo {
      font-weight: 700;
      font-size: 20px;
    }
  }
  i {
    justify-self: end;
    color: white;
    font-size: 20px;
    cursor: pointer;
    @include mixins.sm {
      display: none;
    }
  }
  a.active {
    text-decoration: underline;
  }
  .actions-container {
    @include mixins.xs {
      justify-content: end;
    }
  }

  .menu-xs-container {
    position: relative;
  }

  .menu {
    z-index: 2;
    position: absolute;
    top: 20px;
    right: 0px;
    li {
      padding: 10px;
    }
    a {
      color: var(--text-color);
    }
  }
}
.v-leave-to,
.v-enter-from {
  transform: translateY(-10px);
  opacity: 0;
}

.v-leave-active,
.v-enter-active {
  transition: all 0.2s;
}
</style>
