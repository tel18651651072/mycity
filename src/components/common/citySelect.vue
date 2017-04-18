<template>
    <div class="citySelect-wrapper">
        <label>承保城市:</label>
        <span @click="cityChoice" v-text="selectedCityNew"></span>
    </div>
</template>
<script>
    export default {
        props: {
            selectedCityNew: {
                type: String,
                default: '请选择承保城市...'
            }
        },
        methods: {
            cityChoice() {
                // this.$root.eventHub.$emit('cityChoice', event.target)
                this.$emit('cityChoice')
            }
        }
    }

</script>
<style lang="stylus" rel="stylesheet/stylus">
    .citySelect-wrapper {
        display: flex;
        padding: .4rem .58rem;
        label,
        span {
            flex: 1;
            display: inline-block;
        }
        span {
            text-align: center;
        }
    }
</style>