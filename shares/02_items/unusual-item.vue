<template>
    <div :class="templateClass">
        <h1>{{ content.title }}</h1>
    </div>
</template>

<style lang="less" scoped></style>

<script>
export default {
    mixins: [pckgSmartItem]
}
</script>