<template>
  <footer id="footer" role="contentinfo">
    <div class="footer__inner">
      <!-- Copyright Notice -->
      <div class="footer__copyright">
        <p>
          &copy; 2024 Your Movie Site.<br />
          All rights reserved.<br />
          This site does not generate revenue.
        </p>
      </div>
    </div>
  </footer>
</template>

<style lang="scss">
#footer {
  background-color: #333;
  color: #929292;
  padding: 20px 0;
  text-align: center;
  .footer__copyright {
    flex-grow: 1;
    text-align: center;
    padding-right: 20px; /* Adjust spacing */
  }
}
</style>
