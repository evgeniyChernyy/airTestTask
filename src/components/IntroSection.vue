<script setup>
function openResidentRequestPopup() {
  document.dispatchEvent(new CustomEvent("OpenResidentRequestPopup"))
  document.dispatchEvent(new CustomEvent("ShowOverlay"))
}
</script>

<template>
  <section class="section">
    <div class="container">
      <button class="btn" @click="openResidentRequestPopup">Стать резидентом</button>
    </div>
  </section>
</template>
