<template>
    <header>
        <img :src="logo.mobile" :alt="site.title" class="hidden@sm"/>
        <img :src="logo.mobile" :alt="site.title" class="hidden inline-block@sm" />
        <ul>
            <li v-for="item in menus.frontend.items">
                <router-link :to="item.url">
                    <i v-if="item.icon" class="fal fa-fw" :class="item.icon"></i>
                    {{ item.title }}
                </router-link>
            </li>
        </ul>
        <derive-basket-header v-if="basket.packets.length > 0"></derive-basket-header>
        <p v-else><a href="#">CTA</a></p>
        <slot name="header-slot">
            <component v-for="action in slotElements.headerSlot || []"
                       :action-id="action.id"
                       :is="'pckg-' + action.type"
                       :key="action.id"></component>
        </slot>
    </header>
</template>

<style lang="less" scoped></style>

<script>
export default {
    mixins: [CommsHub.header],
}
</script>
