<template>
    <form @submit.prevent="onSearch" class="w-full">
        <div class="shadow overflow-hidden sm:rounded-md">
status
            <instant-date-range-field label="Created At" :form="form.filters" objprop="created_at" id="created_at"/>
            <instant-input-field label="Name" :form="form.filters" objprop="name" id="name"/>
            <instant-input-field label="Email" :form="form.filters" objprop="email" id="email"/>
            <instant-select-field label="Status" :form="form.filters" objprop="status" id="status" :options="$page.props.status" tags/>
            <instant-button-field>filter</instant-button-field>
        </div>
    </form>
</template>

<script>
    export default {
        data () {
            return {
                form: this.$inertia.form({
                    filters: {
                        created_at: '',
                        status: [''],
                        email: '',
                        name: '',
                    },
                })
            }
        },
        methods: {
            onSearch() {
                this.form.post(this.route('user'), {
                    replace: true,
                    preserveState: true,
                    preserveScroll: false,
                    forceFormData: true,
                    onFinish: () => this.emitter.emit('toggleModal'),
                });
            },
        }
    }
</script>

<style lang="css" scoped>
</style>
