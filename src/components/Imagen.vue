<template>
  <div class="imgoculta">
    <img :src="imagen" alt="La imagen no se pudo cargar" />
    <p>{{ nombre }}</p>
  </div>
</template>

<script>
export default {
  props: {
    imagen: {
      type: String,
      required: true,
    },
    nombre: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
.imgoculta {
  text-align: center;
  object-fit: cover;
}

.imgoculta img {
  width: 100px;
  height: 100px;
}

</style>
