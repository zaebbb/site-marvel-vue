<template>
    <div id="app">

        <app-header :changeSearch="changeSearch"/>

        <div class="container">
            <h1 class="pt-3 pb-3">Персонажи Marvel</h1>

            <app-modal :dataPerson="character" />

            <spinner v-if="loading" />

            <div class="row">

                <h1 v-if="!searchCharacters.length && !loading">Ничего не найдено 😥</h1>

                <div 
                v-for="(el, key) in searchCharacters"
                class="card mb-3  mr-2" 
                style="max-width: 540px; margin-right: 30px"
                :key="key"
                >
                    <div class="row g-0">
                        <div class="col-md-4">
                        <img :src="el.thumbnail" class="img-fluid rounded-start" :alt="el.thumbnail">
                        </div>
                        <div class="col-md-8">
                        <div class="card-body">
                            <h5 class="card-title">{{el.name}}</h5>
                            <p class="card-text">{{el.description.substring(0, 50)}}...</p>
                            <button 
                            class="btn btn-outline-dark w-50" 
                            type="submit" 
                            data-bs-target="#exampleModal" 
                            data-bs-toggle="modal"
                            @click="characterIndex = key"
                            >ПОДРОБНЕЕ</button>
                        </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
    import Spinner from "./components/Spinner";
    import AppModal from "./components/AppModal";
    import AppHeader from "./components/AppHeader";

    export default {
        name: 'App',
        components: {
            AppHeader,
            AppModal,
            Spinner,
        },
        data() {
            return {
                loading: false,
                characters: [],
                characterIndex: 0,
                search: ''
            }
        },
        methods: {
            fetchCharacters: function(){
                return fetch('https://netology-api-marvel.herokuapp.com/characters')
                        .then(res => res.json())
                        .then(json => this.characters = json)
                        .catch(err => err.json())
            },
            changeSearch: function(value){
                this.search = value
            }
        },
        computed: {
            character: function(){
                return this.characters[this.characterIndex] || null
            },
            searchCharacters: function(){
                const {characters, search} = this
                return characters.filter((character) => {
                    return character.name
                        .toLowerCase()
                        .indexOf(search.toLowerCase()) !== -1
                })
            }
        },
        async mounted(){
            this.loading = true
            await this.fetchCharacters()
                this.loading = false
        }
    }
</script>

<style>

</style>
