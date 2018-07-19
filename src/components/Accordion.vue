<template>
    <div class="accordion">
        <slot />
    </div>
</template>

<style scoped>
</style>

<script>
    export default {
        mounted() {
            let details = this.$el.querySelectorAll('details');
            let summaries = this.$el.querySelectorAll('summary');
            summaries.forEach(summary => {
                summary.addEventListener('click', () => {
                    details.forEach(d => d.open = false);
                    // if we let default handling happen no need to set open in fact it will actually break things if we do
                })
            })
        },
        methods: {
            open(indexOrSelector) {
                if (!isNaN(parseInt(indexOrSelector))) {
                    let index = Number(indexOrSelector);
                    let details = this.$el.querySelectorAll('details');
                    details.forEach((d,i) => d.open = index == i);
                } else {
                    throw "Selector based opening of details not yet supported";
                }
            }
        }
    }
</script>