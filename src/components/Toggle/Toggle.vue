<template>
    <div :class="{ 'btn-group': true, 'btn-group-sm': small }">
        <slot />
    </div>
</template>

<style scoped>

</style>

<script>
    import ToggleItem from './ToggleItem'
    export default {
        props: ['value', 'items', 'small' ],
        components: { ToggleItem },
        data: () => ({
            selectedKey: this.value
        }),
        watch: {
            selectedKey(){
                this.$emit('input', this.selectedKey)
            }
        },
        created() {
            this.items = this.$children;
        },
        mounted(){
            this.itemClicked(this.value);
        },
        methods: {
            itemClicked(key) {
                this.selectedKey = key;
                console.log(this.selectedKey)
                this.$children.forEach(item => {
                    item.selected = item.value === key
                });
            }
        }
    }
</script>