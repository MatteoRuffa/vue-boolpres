<template>
    <div class="modal fade" id="staticBackdropInfo" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropInfoLabel" aria-hidden="true">
    <div class="modal-dialog modal-xl">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="staticBackdropInfoLabel">Details</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <h2>{{ project.title }}</h2>
                <p>{{ project.description }}</p>
                <p>{{ project.created_at }}</p>
                <p>{{ project.categories }}</p>
                <p>{{ project.technologies.icon }}</p>
                <p>{{ project.technologies.title }}</p>
                <!-- <p id="modalTypeIdInfo"></p> -->
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            </div>
        </div>
    </div>
</div>
</template>

<script>
    export default {
        name: 'ModalDetails',
        props: ['project'],
        methods: {
            open() {
                this.$nextTick(() => {
                    $('#staticBackdropInfo').modal('show');
                });
            }
        },
        watch: {
            project(newVal) {
                if (newVal) {
                    this.open();
                }
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>