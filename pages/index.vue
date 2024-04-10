<template>
  <v-card title="Home" height="100%"> </v-card>
</template>

<script setup>
definePageMeta({
  middleware: [
    "auth",
  ],
});
</script>

<style lang="scss" scoped></style>
