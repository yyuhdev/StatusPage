<script setup>
import StatusWidget from "@/components/status-widget.vue"

</script>

<template>
  <main>
    <status-widget/>
  </main>

  <footer>
    <div class="footer-container">
      <p class="copy-right">
        yyuh © {{ new Date().getFullYear() }}
      </p>
    </div>
  </footer>
</template>

<style scoped>
</style>
