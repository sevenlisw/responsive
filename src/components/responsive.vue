<template>
    <div class="responsive-wrapper">
        <div class="responsive" id="responsive" :style="responClass">
            <div class="demo-root">
                <header>头部</header>
                <ul>
                    <li class="demo-left">左</li>
                    <li class="demo-center">中</li>
                    <li class="demo-right">右</li>
                </ul>
                <footer>底部</footer>
            </div>
        </div>
        <footer class="large-footer"></footer>
    </div>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
let responClass = ref('')
const handleresponsiveAuto = (): void => {
    const designDraftWidth = 1920;  //设计稿的宽度
    const designDraftHeight = 960;   //设计稿的高度
    const clientWidth = window.innerWidth || document.body.clientWidth// 获取网页可视宽度
    const clientHeight = window.innerHeight || document.body.clientHeight // 获取网页可视高度
    
    //根据屏幕的变化适配的比例
    const scale = clientWidth / clientHeight < designDraftWidth / designDraftHeight ?
        clientWidth / designDraftWidth :
        clientHeight / designDraftHeight;
    //缩放比例
    responClass.value = `transform: scale(${scale}) translate(-50%)`
}

onMounted(() => {
    // 初始化自适应
    handleresponsiveAuto();
    // 绑定自适应函数，防止浏览器变化后不再适配
    window.onresize = () => handleresponsiveAuto();
})

onUnmounted(() => {
    window.onresize = null;
})
</script>

<style lang="scss">
.responsive-wrapper {
    height: 100%;
    width: 100%;

    .responsive {
        display: inline-block;
        width: 1920px;
        transform-origin: 0 0;
        position: absolute;
        left: 50%;

        .demo-root {
            header {
                width: 1920px;
                height: 200px;
                background: rgb(2, 159, 251);
                font-size: 40px;
                text-align: center;
                line-height: 200px;
            }

            ul {
                display: flex;
                height: 660px;

                li {
                    width: 640px;
                    height: 100%;
                    font-size: 40px;
                    line-height: 660px;
                }

                .demo-left {
                    background: rgb(251, 1, 167);
                }

                .demo-center {
                    background: #00ffea;
                }

                .demo-right {
                    background: #c602f7;
                }
            }

            footer {
                width: 100%;
                height: 100px;
                font-size: 40px;
                text-align: center;
                line-height: 100px;
                background: rgba(251, 230, 0, 0.995);
            }
        }
    }
}
</style>