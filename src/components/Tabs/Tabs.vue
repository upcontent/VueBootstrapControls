<template>
    <div class="tabs-component">
        <tab-bar :tabs="tabs" ref="tabBar"></tab-bar>
        <slot />
    </div>
</template>

<style scoped>
</style>

<script>
    import TabBar from './TabBar'
    export default {
        components: { TabBar },
        data() {
            return {
                tabs: []
            }
        },
        mounted() {
            let tabContentElements = this.$children.filter(tab => tab.label);
            let tabBar = this.$refs.tabBar;

            tabBar.$on('tabChange', selectedTab => {
                tabContentElements.forEach(t => {
                    t.isActive = t.label === selectedTab.label;
                });
                this.tabs.forEach(t => {
                    t.active = t.label === selectedTab.label;
                });
            });
            let tabs = tabContentElements.map(tab => ({
                label: tab.label,
                iconClass: tab.iconClass,
                active: tab.active
            }));

            if (!tabs.some(tab => tab.active)) {
                tabs[0].active = true;
                tabContentElements[0].isActive = true;
            }
            this.tabs = tabs;
        }
    }
</script>