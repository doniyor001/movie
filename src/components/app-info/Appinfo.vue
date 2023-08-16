<template>
    <Box>
        <p class="fs-3 text-upercase">Barcha kinolar soni: {{ allMoviesCount }}</p>
        <p class="fs-4 text-upercase">Ko'rilgan kinolar soni:{{ favouriteMoviesCount }} </p>
    </Box>
</template>

<script>
import Box from '@/ui-components/Box.vue';

export default {
    props:{
        allMoviesCount:{
            type:Number,
            required:true,
        },
        favouriteMoviesCount:{
            type:Number,
            required:true,
        },
    },
    components:{
    Box,
}
}
</script>

<style scoped></style>