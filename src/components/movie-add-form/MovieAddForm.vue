<template>
    <box class="movie-add-form">
       <h3>Yangi kino qoshish</h3>
       <form class="add-form d-flex" @submit.prevent>

        <Input
        class="new-movie-label"
        placeholder="Qanday kino?" 
        v-model="name"
        @input="name = $event.target.value"/>

        <Input
          class="new-movie-label"
          placeholder="Nechi marotaba ko'rilgan?"
          type="number"
          v-model="viewers"
          @input="viewers = $event.target.value"/>

          <PrimaryButton 
          class="btn-outline-dark" 
          type="submit" 
          @click="addMovie">Qo'shish</PrimaryButton>

       </form>
    </box>
</template>

<script>
import Input from "@/ui-components/Input.vue";

export default {
    components: {Input},
    data(){
        return{
            name: '',
            viewers: '',
        }
    },
    methods: {
        addMovie() {
            if(!this.name || !this.viewers) return
            const newMovie = {
                name: this.name,
                viewers: this.viewers,
                favourite: false,
                like: false,
                id: Date.now(),
            }
            this.$emit('createMovie', newMovie) //ona divga ma'lumot jo'natish
            this.name = ''
            this.viewers = ''
        },
    },
}
</script>

<style>
</style>