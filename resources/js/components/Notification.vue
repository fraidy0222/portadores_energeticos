<template>
    <div class="text-blue-500" v-if="$page.props.flash.message">
        {{ $page.props.flash.message }}
    </div>
</template>

<script>
export default {
    name: "Notification"
}
</script>

<style scoped>

</style>
