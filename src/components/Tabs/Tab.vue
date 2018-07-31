<template>
    <div :class="{'tab-content': true, active: isActive }">
        <slot />
    </div>
</template>

<style scoped>
    .tab-content {
        display: none;
    }
    .tab-content.active {
        display: block;
    }
</style>

<script>
    export default {
        props: {
            label: String,
            iconClass: String,
            active: Boolean
        },
        data() {
            return {
                isActive: this.active
            }
        }
    }
</script>