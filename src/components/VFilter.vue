<template lang="pug">
  .filter
    .filter__label {{ label }}
    .filter__items
      a.filter__item(
        v-for="filter in filters" :key="filter"
        :class="{'is-active': filter === value}"
        :href="`#${filter}`"
        @click="$emit('change', filter)"
      )
        | {{ filter }}
</template>

<script>
  export default {
    model: {
      prop: 'value',
      event: 'change'
    },
    props: {
      value: {
        type: String,
        required: true
      },
      filters: {
        type: Array,
        required: true
      },
      label: {
        type: String,
        required: true
      }
    },
  }
</script>

<style lang="scss">
.filter {
  display: flex;

  &__label {
    margin-right: 10px;
  }

  &__items {
    display: flex;
  }

  &__item {
    font-family: inherit;
    color: #1C214C;
    text-decoration: none;
    & + & {
      position: relative;
      margin-left: 8px;
      padding-left: 9px;
      &:before {
        content: '';
        display: inline-block;
        position: absolute;
        top: 50%;
        left: 0;
        transform: translateY(-50%);
        width: 1px;
        height: 22px;
        background-color: #DEDEE5;
      }
    }
    &.is-active {
      color: #3E5EF2;
    }
  }
}

</style>
