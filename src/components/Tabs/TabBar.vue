<template>
    <ul class="tab-bar">
        <li :class="{tab:true, active: tab.active}" v-for="tab in tabs" :key="tab.label" @click="tabClick(tab)">
            <div class="tab-bar-tab-content">
                <span class="tab-icon-container">
                    <i :class="tab.iconClass"></i>
                </span>
                <span class="tab-label">{{tab.label}}</span>
            </div>
        </li>
    </ul>
</template>

<style scoped>
    /*ul, ul > li {*/
        /*border-style: solid;*/
        /*border-color: var(--default);*/
    /*}*/
    /*ul      { border-width: 1px  0   0  1px }*/
    /*ul > li { border-width:  0  1px 1px  0  }*/
    .tab-bar {
        background: var(--light);
        border: 1px solid var(--default)
    }
    .tab-bar, .tab { list-style: none; }
    .tab-bar {
        padding-left: 0px;
        display: flex;
        width: 100%;
    }
    .tab {
        display: block;
        padding: 7px 10px 3px 10px;
        text-align: center;
        min-width: 30px;
        max-width: 100%;
        flex-grow: 1;
        cursor: pointer;
    }
    .tab.active {
        border-bottom: 5px solid var(--primary);
    }
    .tab-label {
        display: block;
        text-align: center;
        font-size: .75em;
    }
    .tab-icon-container {
        text-align: center;
        font-size: 1.2em;
    }
    .tab-bar-tab-content {
        text-align: center;
        display: block;
    }
    @media (min-width: 700px) {
        .tab-label {
            display: inline-block;
            text-align: left;
            font-size: 1.1em;
            margin-left: 3px;
        }
        .tab-icon-container {
            text-align: center;
            font-size: 1.1em;
        }
        .tab {
            text-align: left;
            flex-grow: 1;
            padding: 8px 14px 4px 14px;
        }
        /*.tab.active {*/
            /*margin-top:-2px;*/
            /*border-top: 5px solid var(--primary);*/
            /*border-bottom: 1px solid  var(--default);*/
        /*}*/
        /*.tab-bar {*/
            /*margin-top: 5px;*/
        /*}*/
    }
</style>

<script>
    export default {
        props: {
            tabs: Array // { label, iconClass, active }
        },
        methods: {
            tabClick(item) {
                this.$emit('tabChange', item)
            }
        }
    }
</script>