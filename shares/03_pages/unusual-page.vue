<template>
    <div>
        <!-- this is an example of fully featured packet page -->
        <!-- this is rendered to the main content section above content -->
        <!-- it can be added as a single component and wrapped in page builder -->
        <!-- how is this different from the component? -->
        <!-- we probably need some settings here, some things needs to be changed, adapted? -->
        <hub-list-comms-unusual-list :contents="packet.pictures"
                                     :settings="{itemTemplate: 'hub-item-comms-unusual-item'}"></hub-list-comms-unusual-list>

        <div class="flex-grid --grid-num --x2@md">
            <div>

                <!-- packet is required and resolved by the page -->
                <h1>{{ packet.title }}</h1>

                <!-- conditional description -->
                <div class="color-grayish font-size-lg" v-if="packet.description">{{ packet.description }}</div>

                <!-- conditional HTML content -->
                <div class="font-size-md" v-html="packet.content" v-if="packet.content"></div>

                <!-- official component with activated social integrations (FB, TW, LI, IG, ...) -->
                <hub-component-comms-social-like></hub-component-comms-social-like>

            </div>
            <div>

                <!-- native component -->
                <derive-basket-packet-config :initial-packet="packet"></derive-basket-packet-config>

            </div>
            <div v-if="packet.hasAttributes">

                <!-- native component -->
                <derive-packet-attributes :packet="packet"></derive-packet-attributes>

            </div>
            <div v-if="packet.slots.main">

                <!-- native component -->
                <pckg-loop :actions="packet.slots.main"></pckg-loop>

            </div>
            <div v-if="page.slots.last">

                <!-- native component -->
                <pckg-loop :actions="page.slots.last"></pckg-loop>

            </div>
        </div>

        <!-- and some native tabs? -->
        <hub-component-comms-tabs :tabs="[{component: ''}]">

            <!-- attributes -->
            <some-custom-tab name="__('heading.attributes')">
                <custom-packet-attributes-component></custom-packet-attributes-component>
            </some-custom-tab>

            <!-- tab with page slot as content -->
            <some-custom-tab>
                <slot name="foo">
                    <pckg-loop :actions="page.slots.tab"></pckg-loop>
                </slot>
            </some-custom-tab>

            <!-- configurable inquiry form -->
            <some-custom-tab name="Some">
                <derive-form-one :form="page.settings.inquiryForm"></derive-form-one>
            </some-custom-tab>

        </hub-component-comms-tabs>

        <div class="display-block margin-top-md s-similar-packets">
            <h3>{{ __('heading.similarPackets') }}</h3>

            <derive-packets-list :packets="similarPackets"></derive-packets-list>
        </div>

    </div>
</template>

<style lang="less" scoped></style>

<script>
export default {
    mixins: [pckgPage],
    data: function () {
        return {
            // should packet be automatically ORM-ed?
            myPacket: CommsSDK.createRecord('packet', this.packet),
            similarPackets: []
        };
    },
    created: function () {
        this.initialFetch();
    },
    methods: {
        initialFetch: function () {
            this.myPacket.fetchSimilarPackets().then((packets) => {
                this.similarPackets = packets;
            });
        }
    }
}
</script>