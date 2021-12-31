<template lang="html">
  <footer class="footer typography__white-low">
    © Sarragozih by
    <a class="typography__white-low footer__link" href="https://github.com/Dizuite">Dizuite</a>
  </footer>
</template>

<style lang="css" scoped>
.footer {
  padding: 8px 8vw;
  background-color: var(--primary-color);
}

.footer__link {
  border-bottom: 1px solid transparent;
  text-decoration: none;
  transition: .2s;
}

.footer__link:hover {
  border-bottom-color: var(--secondary-color);
  opacity: .6;
}
</style>
