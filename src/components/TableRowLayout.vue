<script>

export default {
  name: 'RowLayout',
}
</script>

<template>
  <li class="row">
    <div class="row__title">
      <div class="row__name">
        <slot name="name"></slot>
      </div>

      <div class="row__phone">
        <slot name="phone"></slot>
      </div>
    </div>

    <slot name="children"></slot>
  </li>
</template>

<style scoped>
img {
  width: 1rem;
  height: 1rem;
}

.row {
  max-width: 25rem;
  text-wrap: wrap;
  word-break: break-word;
}

.row__title {
  border: 1px solid black;
  display: flex;
  justify-content: space-between;
}

.row__title > * {
  padding: 0.5rem;
}

.row__name {
  display: flex;
  align-items: center;
  gap: .2rem;
  word-break: break-all;
}

.row__phone {
  vertical-align: middle;
  max-width: 10rem;
  width: 100%;
  flex-shrink: 0;
  flex-grow: 1;
  border-left: 1px solid black;
}
</style>
