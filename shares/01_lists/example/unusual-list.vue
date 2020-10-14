<template>
    <!-- class "hub-list-comms-unusual-list" is automatically added -->
    <div :class="templateClass">
        <component v-for="(content, i, index) in subcontents"
                   :is="itemComponent"
                   :content="content"
                   :key="content.id"
                   :index="i"
                   :action="myAction"
                   class="__item"></component>
    </div>
</template>

<style lang="less" scoped>
/* can we simplify this to & */
.hub-list-comms-unusual-list {
    .__item {
        width: 50%;
    }
}
</style>

<script>
export default {
    mixins: [pckgSmartList]
}
</script>