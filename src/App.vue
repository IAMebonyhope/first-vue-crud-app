<template>
  <div id="app" class="small-container">
    <h1>Categories</h1>

    <category-form 
      v-if="!isEditMode" 
      @add:category="addCategory"
    />
    <category-edit 
      v-if="isEditMode" 
      :category="category" 
      @edit:category="editCategory"
      @addMode:category="addModeCategory"
    />
    <category-table 
      :categories="categories" 
      @delete:category="deleteCategory"
      @editMode:category="editModeCategory"
    />
  </div>
</template>

<script>
  import CategoryTable from '@/components/CategoryTable.vue'
  import CategoryForm from '@/components/CategoryForm.vue'
  import CategoryEdit from '@/components/CategoryEdit.vue'

  export default {
    name: 'app',
    components: {
      CategoryTable,
      CategoryForm,
      CategoryEdit,
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
        category: {
          name: '',
          description: '',
        },
        isEditMode: false,
      }
    },
    methods: {
      addModeCategory() {
        this.category = {}
        this.isEditMode = false
      },  
      addCategory(category) {
        const lastId = this.categories.length > 0 ? this.categories[this.categories.length - 1].id : 0;
        const id = lastId + 1;
        const newCategory = { ...category, id };

        this.categories = [...this.categories, newCategory]
      },
      deleteCategory(id) {
        this.categories = this.categories.filter(
          category => category.id !== id
        )
      },
      editModeCategory(id) {
        this.category = this.categories[id-1]
        this.isEditMode = true
      },  
      editCategory(id, updatedCategory) {
        this.categories = this.categories.map(category =>
          category.id === id ? updatedCategory : category
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