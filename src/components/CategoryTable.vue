<template>
  <div id="category-table">
    <p v-if="categories.length < 1" class="empty-table">
      No Category
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>Category Name</th>
          <th>Category Description</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="category in categories" :key="category.id">
          <td>{{ category.name }}</td>
          <td>{{ category.description }}</td>
          <td>
            <button>Edit</button>
            <button @click="$emit('delete:category', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'category-table',
    props: {
      categories: Array,
    },
  }
</script>

<style scoped></style>