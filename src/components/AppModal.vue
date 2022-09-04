<template>
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel">{{dataPerson.name}}</h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <img :src="dataPerson.thumbnail" class="img-fluid mb-4" alt="...">
                <h5>Описание</h5>
                <p>{{dataPerson.description}}</p>
                <h5>Комиксы:</h5>
                <ul>
                    <li v-for="(comic, key) in dataPerson.comics" :key="key">
                        <a target="_blank" style="color: #202020; text-decoration: none;" :href="comic.resourceURI">{{comic.name}}</a>
                    </li>
                </ul>
                
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-outline-dark" data-bs-dismiss="modal">ЗАКРЫТЬ</button>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
    export default {
        name: "AppModal",
        props: [
            "dataPerson"
        ]
    }
</script>

<style scoped>

</style>
