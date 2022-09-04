<template>
    <nav class="navbar navbar-dark bg-dark">
        <div class="container">
          <a class="navbar-brand" href="#">ZAEBMARVEL</a>
          <form class="d-flex w-50 justify-content-end">
            <input 
              class="form-control me-2 w-50" 
              type="search" 
              placeholder="Фильтр" 
              aria-label="Search"
              v-model="search"
              @input="changeSearch(search)"
            >
            <button 
              class="btn btn-outline-light w-25" 
              @click="() => {search='';changeSearch(search)}"
              type="reset"
            >СБРОСИТЬ</button>
          </form>
        </div>
      </nav>
</template>

<script>
    export default {
        name: "AppHeader",
        props: ['changeSearch'],
        data() {
            return {
                search: ''
            }
        },
    }
</script>

<style scoped>

</style>
