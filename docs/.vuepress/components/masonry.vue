<template>
  <div
    class="masonry"
  >
    <slot/>
  </div>
</template>

<style lang="stylus">
  .masonry
    column-count 3
    column-gap 0
    & > *
      break-inside avoid
      box-sizing border-box
      counter-increment: item-counter;
</style>