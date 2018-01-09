<template>
    <mu-flexbox orient="vertical" align="stretch" class="park-tab">
        <div class="canvas-box" id="canvas-box" style="background-color: seagreen">
        </div>
        <div>
            <mu-menu-item title="停车位数量">
                <mu-badge content="120" color="green" slot="after"/>
            </mu-menu-item>
            <mu-menu-item title="剩余停车位">
                <mu-badge content="12" color="green" slot="after"/>
            </mu-menu-item>
            <mu-menu-item v-if="parkStatus" title="您的车停在">
                <mu-badge content="12" color="blue" slot="after"/>
            </mu-menu-item>
            <div v-if="!parkStatus">
                <mu-raised-button class="button-box" node-type="qr-btn" label="扫码停车哦"  fullWidth primary/>
            </div>
            <div v-else>
                <mu-raised-button class="button-box" label="扫码定位当前位置" fullWidth primary/>
                <mu-raised-button class="button-box" label="结账开走" @click="openPaySheet" fullWidth primary/>
            </div>
            <input id="car" node-type="jsbridge" type="file" name="myPhoto" value="扫描二维码1"  v-show="false">
        </div>
        <mu-bottom-sheet :open="parkSheet" @close="closeParkSheet">
            <mu-sub-header>
                确认您的停车信息
            </mu-sub-header>

            <mu-list-item title="停车号">
                <mu-badge :content="pos" slot="after"/>
            </mu-list-item>
            <mu-list-item title="其他信息">
            </mu-list-item>
            <mu-flat-button label="确定停车" @click="park(pos)" style="width: 100%" primary/>
        </mu-bottom-sheet>
        <mu-bottom-sheet :open="paySheet" @close="closePaySheet">
            <mu-sub-header>
                确认您的停车信息
            </mu-sub-header>

            <mu-list-item title="停车号">
                <mu-badge :content="pos" slot="after"/>
            </mu-list-item>
            <mu-list-item title="停车时间">
                <mu-badge :content="pos" slot="after"/>
            </mu-list-item>
            <mu-list-item title="开走时间">
                <mu-badge :content="pos" slot="after"/>
            </mu-list-item>
            <mu-list-item title="支付金额">
                <mu-badge :content="pos" slot="after"/>
            </mu-list-item>
            <mu-flat-button label="支付宝支付" @click="pay(pos)" style="width: 100%" primary/>
        </mu-bottom-sheet>
        <mu-toast v-if="toast" message="停车成功" @close="hideToast"/>
    </mu-flexbox>
</template>

<script>
    import Qrcode from '../assets/js/qrcode'
    export default {
        name: '',
        data() {
            return {
                parkStatus: false,
                parkSheet: false,
                paySheet: false,
                pos: 12,
                toast: false,
                cameraInput: null
            }
        },
        mounted: function () {
            $(function () {
                Qrcode.init($('[node-type=qr-btn]'));
            });
            this.cameraInput = document.getElementById('car')
        },
        methods: {
            park(pos) {
                this.showToast()
                this.closeParkSheet()
                this.parkStatus = true
            },
            pay() {

            },
            openCamera() {
                this.cameraInput.click()
            },
            closeParkSheet() {
                this.parkSheet = false
            },
            openParkSheet() {
                if (this.cameraInput.files.length === 1) {
                    this.parkSheet = true
                }
            },
            showToast() {
                this.toast = true
                if (this.toastTimer) clearTimeout(this.toastTimer)
                this.toastTimer = setTimeout(() => {
                    this.toast = false
                }, 2000)
            },
            openPaySheet() {
                this.paySheet = true
            },
            closePaySheet() {
                this.paySheet = false
            }
        }
    }
</script>

<style>
    .park-tab {
        height: 100%;
    }

    .canvas-box {
        flex-grow: 2;
    }

    .button-box {
        margin: 5px 0;
    }
</style>
