<script setup>
defineProps(["title", "body","id"]);

</script>

<template>
  <div class="card mt-3 mb-3">
    <div class="card-body border border-success-subtle">
      <h5>{{ id }} {{ title }}</h5>
      <p>
        {{ body }}
      </p>
      <button class="btn btn-outline-primary" @click="$emit('cambiarfavorito', title)">Favorito</button>
    </div>
  </div>
</template>
<style></style>
