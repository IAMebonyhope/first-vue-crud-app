<template>
  <div id="app" class="small-container">
    <h1>Categories</h1>

    <category-form @add:category="addCategory"/>
    <category-table :categories="categories" @delete:category="deleteCategory"/>
  </div>
</template>

<script>
  import CategoryTable from '@/components/CategoryTable.vue'
  import CategoryForm from '@/components/CategoryForm.vue'

  export default {
    name: 'app',
    components: {
      CategoryTable,
      CategoryForm,
    },
    data() {
      return {
        categories: [
          {
            id: 1,
            name: 'nusery',
            description: 'no description',
          },
          {
            id: 2,
            name: 'primary',
            description: 'no description',
          },
          {
            id: 3,
            name: 'junior',
            description: 'no description',
          },
        ],
      }
    },
    methods: {
      addCategory(category) {
        const lastId = this.categories.length > 0 ? this.categories[this.categories.length - 1].id : 0;
        const id = lastId + 1;
        const newCategory = { ...category, id };

        this.categories = [...this.categories, newCategory]
      },
      deleteCategory(id) {
        this.category = this.categories.filter(
          category => category.id !== id
        )
      }
    }
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>