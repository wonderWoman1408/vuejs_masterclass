<template>
    <div>
        <ForumListItem 
            v-for="forum in forums"
            :forum="forum"
            :key="forum['.key']"
        />

    </div>

</template>

<script>
import ForumListItem from '@/components/ForumListItem.vue';

export default {
    components: {
        ForumListItem
    },
    props: {
        forums: {
            required: true,
            type: Array
        }
    }
};
</script>

<style scoped>

</style>