<template>
    <div class="progress">
        <div 
            class="progress-bar progress-bar-striped progress-bar-animated" 
            role="progressbar" 
            aria-valuenow="99" 
            aria-valuemin="0" 
            aria-valuemax="100" 
            style="width: 100%"
        ></div>
    </div>
</template>

<script>
export default {
    props : [],
    data(){
        return {

        }
    },
    mounted(){

    },
    methods : {

    }
}
</script>

<style scoped>
.progress {
    margin-bottom: 10px;
}
.progress-bar-striped {
    background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.35) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.35) 50%, rgba(255, 255, 255, 0.35) 75%, transparent 75%, transparent);
    background-size: 1rem 1rem;
}
</style>