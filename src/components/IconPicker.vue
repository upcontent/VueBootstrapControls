<template>
    <div class="input-group icon-picker">
        <span class="input-group-prepend">
                <span class="input-group-text">
                    <i :class="icon.style"></i>
                </span>
        </span>
        <v-select :options="icons"  v-model="icon" class="icon-dropdown">
            <template slot="option" slot-scope="option">
                <span class="icon-container">
                    <i :class="option.style"></i>
                </span>
                {{ option.label }}
            </template>
        </v-select>
    </div>
</template>

<style>
   .icon-picker .icon-container {
       margin-right: .75em;
       width: 1em;
       display: inline-block;
       text-align: center;
   }
   .input-group.icon-picker .form-control,
   .input-group.icon-picker .dropdown-toggle  {
       border-top-left-radius: 0;
       border-bottom-left-radius: 0;
   }

   .icon-picker .input-group-prepend .input-group-text {
       width: 40px;
   }

   .icon-picker .icon-dropdown {
       width: calc(100% - 40px);
   }

   .input-group.icon-picker {
        width: 100%;
    }
</style>

<script>
    import {VueSelect} from 'vue-select'
    export default {
        components: { vSelect: VueSelect },
        props: {
            icons: Array, // { value: String, style: String, label: String },
            value: String
        },
        data() {
            return {
                icon: this.icons.find(i => i.key === this.value) || ''
            }
        },
        watch: {
            icon() {
                console.log(this.icon)
                this.$emit('input', this.icon.value)
            }
        }
    }
</script>