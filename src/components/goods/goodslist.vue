<template>
    <div class="tmpl">
        <!-- 面包屑导航 -->
        <div class="section">
            <div class="location">
                <span>当前位置：</span>
                <a href="/index.html">首页</a> &gt;
                <a href="/goods.html">购物商城</a>
            </div>
        </div>

        <div class="section">
            <div class="wrapper">
                <div class="wrap-box">
                    <!--类别菜单-->
                    <div class="left-220" style="margin:0;">
                        <div class="banner-nav">
                            <ul>
                                <!--此处声明下面可重复循环-->

                                <li v-for="item in topinfo.catelist  ">
                                    <h3>
                                        <i class="iconfont icon-arrow-right"></i>
                                        <span>{{item.title}}</span>
                                        <p>
                                            <span v-for="subitem in item.subcates" :key="item.id">
                                                {{subitem.title}}&nbsp;
                                            </span>
                                        </p>
                                    </h3>
                                    <div class="item-box">
                                        <!--如有三级分类，此处可循环-->
                                        <dl>
                                            <dt>
                                                <a href="/goods/40.html">{{item.title}}</a>
                                            </dt>
                                            <dd>
                                                <span v-for="subitem in item.subcates" :key="item.id">
                                                    <a href="/goods/44.html">{{subitem.title}}</a>
                                                </span>
                                            </dd>
                                        </dl>
                                    </div>
                                </li>

                            </ul>
                        </div>
                    </div>
                    <!--/类别菜单-->

                    <!--幻灯片-->
                    <div class="left-705">
                        <div class="banner-img">
                            <template>
                                <el-carousel arrow="always" interval="5000" indicator-position="outside">
                                    <el-carousel-item v-for="item in topinfo.sliderlist" :key="item.id">
                                        <img width="368" height="368" :src="item.img_url" alt="">
                                        <h3>{{item.title}}</h3>
                                    </el-carousel-item>
                                </el-carousel>
                            </template>

                        </div>
                    </div>
                    <!--/幻灯片-->

                    <!--推荐商品-->
                    <div class="left-220">
                        <ul class="side-img-list">

                            <li v-for="(item,index) in topinfo.toplist" ::key="item.id">
                                <div class="img-box">
                                    <label>1</label>
                                    <img src="item.img_url">
                                </div>
                                <div class="txt-box">
                                    <a href="/goods/show-98.html">{{item.title}}</a>
                                    <span>2015-04-20</span>
                                </div>
                            </li>
                        </ul>
                    </div>
                    <!--/推荐商品-->

                    <div class="section" v-for="item in list" :key="item.level1cateid">

                        <!--子类-->
                        <div class="main-tit" >
                            <h2>{{item.catetitle}}</h2>
                            <p >
                                <a v-for = "subitem in item.level2catelist" :key="subitem.subcateid" href="/goods/43.html">
                                    {{subitem.subcatetitle}}
                                </a>
                                <a href="/goods/40.html">更多
                                    <i>+</i>
                                </a>
                            </p>
                        </div>
                        <!--/子类-->
                        <div class="wrapper clearfix">
                            <div class="wrap-box">
                                <ul class="img-list">

                                    <li v-for="subitem in item.datas">
                                        <a href="/goods/show-91.html">
                                            <div class="img-box">
                                                <img src="subitem.img_url">
                                            </div>
                                            <div class="info">
                                                <h3>{{subitem.artTitle}}</h3>
                                                <p class="price">
                                                    <b>¥{{subitem.sell_price}}</b>元</p>
                                                <p>
                                                    <strong>库存 {{subitem.stock_quantity}}</strong>
                                                    <span>市场价：
                                                        <s>{{subitem.market_price}}</s>
                                                    </span>
                                                </p>
                                            </div>
                                        </a>
                                    </li>


                                </ul>
                            </div>
                        </div>
                    </div>


                </div>
            </div>
        </div>



    </div>
</template>

<script>
    export default {
        data() {
            return {
                // 负责存储商品列表页面的顶部区域的数据
                // 格式： {catelist: 分类数据数组,sliderlist: 轮播图数据数组 ,toplist:推荐商品数据数组 }
                topinfo: [],
                list:[]
            }
        },
        mounted() {
            this.gettopinfo()
            this.getlist()
        },
        methods: {
            // 2.0 获取页面底部的商品数据        
            getlist(){
                var url ="/site/goods/getgoodsgroup";
                this.$ajax.get(url)
                          .then(res=>{
                              this.list = res.data.message;
                          })  
            },
            
        // 1.0 获取页面顶部三块区域的数据
        gettopinfo() {
                var url = "/site/goods/gettopdata/goods";
                this.$ajax.get(url)
                    .then(res => {
                        this.topinfo = res.data.message;
                    })
            }
        },
    }

</script>
<style>
    .el-carousel__container {
        height: 368px;
        color: red;
    }

    .el-carousel__item h3 {
        color: red;
        font-size: 18px;
        opacity: 0.75;
        line-height: 50px;
        margin: 0;
    }

    .el-carousel__item:nth-child(2n) {
        background-color: #99a9bf;
    }

    .el-carousel__item:nth-child(2n+1) {
        background-color: #d3dce6;
    }
</style>