<template>
    <div class="multi-select">
        <multi-select v-model="selectedItems"></multi-select>
        <select v-model="newItem" class="form-control input-sm"
                :placeholder="placeholder"
                @keyup.enter="additem" @change="addItem" maxlength="20" >
            <option v-for="item in items" :key="item">{{item}}</option>
        </select>
    </div>
</template>

<script>
    import MultiSelect from './MultiSelection'
    export default {
        props : ['value', 'items', 'placeholder'],
        components: { MultiSelect },
        data(){
            return {
                newItem : '',
                itemToAdd: '',
                selectedItems : this.value
            }
        },
        watch: {
            selectedItems(){
                this.$emit('input', this.selectedItems)
            },
        },
        mounted(){
            this.selectedItems = this.value;
        },
        methods : {
            addItem(){
                if (this.newItem && this.selectedItems.indexOf(this.newItem)  == -1)
                    this.selectedItems.push(this.newItem);
                this.newItem = '';
            },
            removeItem(item){
                this.selectedItems = this.selectedItems.filter(i => i !== item);
            }
        }
    }
</script>

<style scoped>
</style>