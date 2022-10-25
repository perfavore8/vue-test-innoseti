<template>
  <div class="about">
    <slot />
  </div>
</template>

<style lang="scss" scoped>
.about {
  width: 100%;
  padding: 2em;
  display: flex;
  flex-direction: column;
  gap: 4em;
}
</style>
