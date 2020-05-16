<template>
    <div id="category-edit">
        <form @submit.prevent="handleEdit">
            <label>Category Name</label>
            <input 
                type="text" 
                :class="{ 'has-error': submitting && invalidName }"
                @focus="clearStatus"
                @keypress="clearStatus"
                v-model="category.name"
            />

            <label>Category Description</label>
            <input 
                type="text" 
                :class="{ 'has-error': submitting && invalidDesc }"
                @focus="clearStatus"
                @keypress="clearStatus"
                v-model="category.description"
            />

            <p v-if="error && submitting" class="error-message">
                ❗Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                ✅ Category successfully updated
            </p>
            
            <button>Update Category</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'category-edit',
        props: {
            category: Object,
            isEditMode: Boolean,
        },
        data() {
            return {
                submitting: false,
                error: false,
                success: false,
                
            }
        },
        methods: {
            handleEdit() {
                this.submitting = true
                this.clearStatus()

                if (this.invalidName || this.invalidDesc) {
                    this.error = true
                    return
                }

                this.$emit('edit:category', this.category.id, this.category)
                this.category = {
                    name: '',
                    description: '',
                }

                this.error = false
                this.success = true
                this.submitting = false

                this.changeMode()
            },
            clearStatus() {
                this.success = false
                this.error = false
            },
            changeMode() {
                this.$emit('addMode:category')
            }
        },
        computed: {
            invalidName() {
                return this.category.name === ''
            },

            invalidDesc() {
                return this.category.description === ''
            },
        },
    }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>