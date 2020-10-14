<template>
    <div>{{ counter }}</div>
</template>

<style lang="less" scoped></style>

<script>
export default {
    mixin: [pckgComponent],
    comms: {
        settings: ['from', 'to', 'speed']
    },
    data: function () {
        /**
         * pckgComponent.data already collects settings? And sets watcher?
         */
        return Object.assign(pckgComponent.data.call(this), {
            counter: null,
            step: null
        },/*this.settings(['from', 'to', 'speed'])*/);
    },
    methods: {
        calculateParams: function () {
            if (this.setting.from === this.setting.to) {
                return;
            }
            this.counter = this.setting.from;

            let diff = this.setting.to - this.setting.from;
            this.step = diff / 100;
        },
        continueCounter: function () {
            if (!this.step) {
                return;
            }
            setTimeout(() => {
                this.value += this.step;
                if ((this.step > 0 && this.value >= this.setting.to) || (this.step < 0 && this.value <= this.setting.to)) {
                    this.continueCounter();
                }
            }, 100);
        }
    },
    created: function () {
        this.calculateParams();
    },
    mounted: function () {
        this.continueCounter();
    }
}
</script>