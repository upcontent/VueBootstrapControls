<template>
    <div v-if="selectedItems.length" class="d-flex flex-wrap mt-1">
        <span class="label" v-for="item in selectedItems" :key="'item-'+item">{{item}} <i class="fa fa-remove" @click="removeitem(item)"></i></span>
    </div>
</template>

<script>
    export default {
        props : ['value'],
        data(){
            return {
                selectedItems : this.value
            }
        },
        watch: {
            selectedItems(){
                this.$emit('input', this.selectedItems)
            }
        },
        mounted(){
            this.selectedItems = this.value;
        },
        methods : {
            removeitem(item){
                this.selectedItems = this.selectedItems.filter(i => i !== item);
            }
        }
    }
</script>

<style scoped>
    span.label {
        background: #75578e;
        color: white;
        margin-right: 4px;
        font-size: 12px;
        padding: 0.1rem 0.5rem;
        border-radius: 3px;
        margin-bottom: 4px;
    }
    .fa.fa-remove {
        cursor: pointer;
    }
</style>