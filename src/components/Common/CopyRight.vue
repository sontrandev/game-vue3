<template>
  <p class="copyright">This game owed by SHK Team in Vue 3 course beginners - <a href="#">View here</a></p>
</template>

<style lang="css" scoped>
  .copyright {
    position: fixed;
    left: 50%;
    transform: translateX(-50%);
    bottom: 1.5rem;
    color: var(--light);
    z-index: 3;
    font-size: 1.5rem;
  }

  .copyright a {
    color: #f4dc26;
  }
</style>