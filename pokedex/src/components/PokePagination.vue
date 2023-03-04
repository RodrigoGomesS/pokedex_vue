<template>
  <v-pagination v-model="currentPage" :length="Math.ceil(filteredItems.length / itemsPerPage)" :total-visible="10"
    circle />
</template>
  
<script>
export default {
  name: 'PokePagination',

  props: {
    items: {
      type: Array,
      required: true
    },
    filterValue: {
      type: String,
      default: ''
    },
    itemsPerPage: {
      type: Number,
      default: 12
    },
    page: {
      type: Number,
      required: true
    }
  },

  computed: {
    filteredItems() {
      if (this.filterValue) {
        return this.items.filter((item) =>
          item.name.toLowerCase().includes(this.filterValue)
        );
      } else {
        return this.items;
      }
    },
    currentPage: {
      get() {
        return this.page;
      },
      set(value) {
        this.$emit('update:page', value);
      }
    }
  }
};
</script>
  