<template>
    <div class="goodsinfo-container">
        <!-- 商品轮播图区域 -->
        <div class="mui-card">
            <div class="mui-card-content">
                <div class="mui-card-content-inner">
                    <swiper :lunbotuList="lunbotu" :isfull="false"></swiper>
                </div>
            </div>
        </div>
        <!-- 商品购买区域 -->
        <div class="mui-card">
            <div class="mui-card-header">商品名</div>
            <div class="mui-card-content">
                <div class="mui-card-content-inner">
                    <p class="price">
                        市场价：<del>￥2399</del>&nbsp;&nbsp;
                        销售价：<span class="now_price">￥236</span>
                    </p>
                    <p>购买数量：
                        <numberbox></numberbox>
                    </p>
                    <p>
                        <mt-button type="primary" size="small">立即购买</mt-button>
                        <mt-button type="danger" size="small">加入购物车</mt-button>
                    </p>
                </div>
            </div>
        </div>
        <!-- 商品参数区域 -->
        <div class="mui-card">
            <div class="mui-card-header">页眉</div>
            <div class="mui-card-content">
                <div class="mui-card-content-inner">
                    包含页眉页脚的卡片，页眉常用来显示面板标题，页脚用来显示额外信息或支持的操作（比如点赞、评论等）
                </div>
            </div>
            <div class="mui-card-footer">页脚</div>
        </div>
    </div>
</template>

<script>
    import swiper from '../subcomponents/swiper.vue'
    import numberbox from '../subcomponents/goodsinfo_numberbox.vue'
    export default {
        name: "GoodsInfo",
        data() {
            return {
                id: this.$route.params.id, // 将路由参数对象中的 id 挂载到 data , 方便后期调用
                lunbotu: [], // 轮播图的数据
            }
        },
        created() {
           this.getLunbotu();
        },
        methods: {
            getLunbotu() {
               this.$http.get("api/getthumimages/" + this.id).then(result => {
                   if (result.body.status === 0) {
                       // 先循环轮播图数组的每一项，为 item 添加 img 属性，因为 轮播图 组件中，只认识                                 item.img， 不认识 item.src
                       result.body.message.forEach(item => {
                           item.img = item.src;
                       });
                       this.lunbotu = result.body.message;
                   }
               })
           }
        },
        components: {
            swiper,
            numberbox
        }
    }
</script>

<style lang="scss" scoped>
.goodsinfo-container {
    background-color: #eee;
    overflow: hidden;

    .now_price {
        color: red;
        font-size: 16px;
        font-weight: bold;
    }
}
</style>