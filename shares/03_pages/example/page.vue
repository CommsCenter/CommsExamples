<template>
    <div>
        <!-- this is an example of fully featured packet page -->
        <!-- this is rendered to the main content section -->
        <!-- it can be added as a single component and wrapped in page builder -->
        <!-- how is this different from the component? -->
        <!-- we probably need some settings here, some things needs to be changed, adapted? -->
        <hub-list-vendor-some-gallery :pictures="packet.pictures"></hub-list-vendor-some-gallery>

        <h1>{{ packet.title }}</h1>

        <div class="color-grayish font-size-lg">{{ packet.description }}</div>

        <div class="font-size-md" v-html="packet.content"></div>

        <some-custom-tabs>
            <some-custom-tab name="Some">
                <some-contact-form></some-contact-form>
            </some-custom-tab>
            <some-custom-tab name="Some">
                <custom-packet-attributes-component></custom-packet-attributes-component>
            </some-custom-tab>
            <some-custom-tab>
                <slot name="foo"></slot>
            </some-custom-tab>
        </some-custom-tabs>
    </div>
</template>

<style lang="less" scoped></style>

<script>
export default {}
</script>