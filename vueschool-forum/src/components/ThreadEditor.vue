<template>
    <form @submit.prevent="save">
        <div class="form-group">
        <label for="thread_title">Title:</label>
        <input v-model="forum.title" type="text" id="thread_title" class="form-input" name="title">
        </div>

        <div class="form-group">
        <label for="thread_content">Content:</label>
        <textarea v-model="forum.text" id="thread_content" class="form-input" name="content" rows="8" cols="140"></textarea>
        </div>

        <div class="btn-group">
        <button @click.prevent="cancel" class="btn btn-ghost">Cancel</button>
        <button class="btn btn-blue" type="submit" name="Publish">{{isUpdate ? 'Update' : 'Publish'}}</button>
        </div>
    </form>
</template>

<script>
    export default {
        props: {
            title: {
                type: String,
                default: ''
            },
            text: {
                type: String,
                default: ''
            }
        },
        data() {
            return {
                forum: {
                    title: this.title,
                    text: this.text
                }
            }
        },
        computed: {
            isUpdate() {
                return !!this.title;
            }
        },
        methods: {
            save() {
                this.$emit('save', {title: this.forum.title, text: this.forum.text});
            },
            cancel() {
                this.$emit('cancel');
            }
        },
    }
</script>