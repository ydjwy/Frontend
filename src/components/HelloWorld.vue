<template>
    <div class="hello">
        <div id="apiBox"></div>
        <div class="img_box" v-for="(img,index) in imgList" :key="index">
            <img :src="img" alt="">
        </div>
        <div v-if="isShowScape" id="scapeBox">
            <div>
                <img src="../assets/scape.png" alt="">
                <p style="color:#ffffff;margin-top: 40px">请使用横屏的访问</p>
            </div>
        </div>
    </div>
</template>

<script>
    const image = require('../assets/img.jpg');
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data(){
            return {
                imgList: [image, image, image, image, image, image, image, image],
                isShowScape: false
            }
        },
        created(){

            //  ajax请求接口
            function loadXMLDoc() {
                var xmlhttp;
                if (window.XMLHttpRequest) {
                    xmlhttp = new XMLHttpRequest();
                }
                xmlhttp.onreadystatechange = function () {
                    if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
                        document.getElementById("apiBox").innerHTML = xmlhttp.responseText;
                    }
                }
                xmlhttp.open("GET", "/api/api.txt", true);
                xmlhttp.send();
            }

            loadXMLDoc();

            //   横竖屏处理
            if (window.orientation == 180 || window.orientation == 0) {
                this.isShowScape = true;
            }
            window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize",    //判断手机横竖屏状态：
                () => {
                    if (window.orientation == 180 || window.orientation == 0) {
                        this.isShowScape = true;
                    }
                    if (window.orientation == 90 || window.orientation == -90) {
                        this.isShowScape = false;
                    }
                }, false);
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .img_box {
        float: left;
        width: 100%;
    }

    .img_box img {
        width: 100%;
    }

    /* Extra small devices (phones, 600px and down) */
    @media only screen and (max-width: 600px) {
        .img_box {
            width: 100%;
        }
    }

    /* Small devices (portrait tablets and large phones, 600px and up) */
    @media only screen and (min-width: 600px) {
        .img_box {
            width: 100%;
        }
    }

    /* Medium devices (landscape tablets, 768px and up) */
    @media only screen and (min-width: 768px) {
        .img_box {
            width: 50%;
        }
    }

    /* Large devices (laptops/desktops, 992px and up) */
    @media only screen and (min-width: 992px) {
        .img_box {
            width: 25%;
        }
    }

    /* Extra large devices (large laptops and desktops, 1200px and up) */
    @media only screen and (min-width: 1200px) {
        .img_box {
            width: 25%;
        }
    }

    #scapeBox {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        background-color: #000000;
        opacity: 0.5;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #scapeBox img {
        width: 50%;
        animation: myMove 1s infinite;
    }

    @keyframes myMove {
        from {
            transform: rotate(0deg);
        }
        to {
            transform: rotate(90deg);
        }
    }
</style>
