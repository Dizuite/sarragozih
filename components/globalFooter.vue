<template lang="html">
  <footer class="footer">
    <span class="typography__white-low">
      © Sarragozih by
      <a class="typography__white-low footer__link" href="https://github.com/Dizuite">Dizuite</a>
    </span>
  </footer>
</template>

<script>
export default {
  props: ['data'],
}
</script>

<style lang="css" scoped>
.footer {
  width: calc(100% - 16vw);
  padding: 8px 8vw;
  background-color: var(--primary-color);
}

.footer__link {
  border-bottom: 1px solid var(--primary-color);
  text-decoration: none;
  transition: .2s;
}

.footer__link:hover {
  border-bottom: 1px solid var(--secondary-color);
  opacity: .6;
}
</style>
