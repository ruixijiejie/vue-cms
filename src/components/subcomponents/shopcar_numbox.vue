<template>
    <div class="mui-numbox" data-numbox-min='1' style="height: 25px">
        <button class="mui-btn mui-btn-numbox-minus" type="button">-</button>
        <input id="test" class="mui-input-numbox" type="number" :value="initcount" @change="countChanged" ref="numbox" readonly/>
        <button class="mui-btn mui-btn-numbox-plus" type="button">+</button>
    </div>
</template>

<script>
    import mui from '../../lib/mui/js/mui.min.js'
    export default {
        name: "shopcar_numbox",
        methods: {
            countChanged() {
                // 数量改变了
                // console.log(this.$refs.numbox.value);
                // 每当数量值改变，则立即把最新的数量同步到 购物车的  store 中，覆盖之前的数量值
                this.$store.commit("updateGoodsInfo", {
                    id: this.goodsid,
                    count: this.$refs.numbox.value
                });
            }
        },
        props: ["initcount", "goodsid"],
        mounted() {
            // 初始或数字选择框
            mui(".mui-numbox").numbox();
            console.log(this.max);
        }
    }
</script>

<style scoped>

</style>