<template>
    <div data-frontend>
        <main>
            <component v-for="action in groupedRootElements.content"
                       :action-id="action.id"
                       :is="'pckg-' + action.type"
                       :key="action.id"></component>
        </main>
        <main>
            <component v-for="action in groupedRootElements.content"
                       :action-id="action.id"
                       :is="'pckg-' + action.type"
                       :key="action.id"></component>
        </main>
        <aside>
            <component v-for="action in groupedRootElements.sidebar"
                       :action-id="action.id"
                       :is="'pckg-' + action.type"
                       :key="action.id"></component>
        </aside>
        <footer>
            <component v-for="action in groupedRootElements.footer"
                       :action-id="action.id"
                       :is="'pckg-' + action.type"
                       :key="action.id"></component>
        </footer>
    </div>
</template>

<style lang="less" scoped>

</style>

<script>
export default {
    mixins: [pckgLayout],
    computed: {
        groupedActions: function () {
            return [
                $store.getters.groupedRootElements.header,
                $store.getters.groupedRootElements.content,
                $store.getters.groupedRootElements.footer
            ];
        }
    }
}
</script>