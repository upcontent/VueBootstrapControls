<template>
    <div class="modal fade" ref="modal" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <header class="modal-header">
                    <slot name="header" />
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </header>
                <main class="modal-body">
                    <slot />
                </main>
                <footer class="modal-footer">
                    <slot name="footer"/>
                </footer>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .modal-header h5,
    .modal-header h4,
    .modal-header h3,
    .modal-header h2,
    .modal-header h1  {
        margin: 0;
    }
</style>

<script>
    import * as $ from 'jquery';
    export default {
        methods: {
            show() {
                $(this.$refs.modal).modal('show');
            },
            hide() {
                $(this.$refs.modal).modal('hide');
            }
        }
    }
</script>