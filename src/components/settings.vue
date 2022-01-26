<template>

    <div
        class="nav"
        @mousedown.stop
    >
        <img
            class="gear-icon"
            src="../assets/settings-gear.png"
            alt="gear-icon"
            @click="showModal = !showModal"
            draggable="false"
        />
        <div
            class="box"
            v-if="showModal"
        >
            <div style="display:flex; flex-direction: column; align-items: center; margin-top: 30px">
                <p>Orientation:</p>
                <div class="orientation-select">
                    <img
                        draggable="false"
                        @click="this.orientationRotate = !this.orientationRotate, emitOrientation()"
                        :style="`transform: rotate(${this.orientationRotate ? '-90deg' : '0deg'})`"
                        src="../assets/orientation.png"
                        alt="orientation"
                    />
                </div>
            </div>
            
            <p class="credit" style="font-size: 12px;">
                Created by: 
                <a
                    href="https://www.brianfordcode.com"
                    target="_blank">Brian Ford
                </a>
            </p>
        </div>
    </div>

</template>

<script>
export default {
    data() {
        return {
            showModal: false,
            orientationRotate: true,
            currentOrientation: '',
            size: 0
        }
    },
    mounted() {
        const clickAwayHandler = () => {
            this.showModal = false;
        }
        document.body.addEventListener('mousedown', clickAwayHandler)
    },
    methods: {
        emitOrientation() {
            this.orientationRotate ? this.currentOrientation = 'column' : this.currentOrientation = 'row'
            this.$emit('change', this.currentOrientation)
            return this.currentOrientation
        },
    }
}
</script>

<style scoped>
    .nav {
        width: 100vw;
        display: flex;
        justify-content: flex-end;
        /* border: 1px solid blue; */
    }

    .gear-icon {
        height: 25px;
        top: 20px;
        right: 20px;
        margin: 20px 20px 0 20px;
        transition: 1s ease-in-out;
        cursor: pointer;
    }

    .gear-icon:hover {
        transform: rotate(180deg);
    }

    .box {
        z-index: 100000;
        position: absolute;
        display: flex;
        justify-content: space-around;
        align-items: flex-start;
        right: 20px;
        top: 50px;
        height: 150px;
        width: 200px;
        border-radius: 10px;
        background-color: rgba(0,0,0,0.95);
        box-shadow: 0px 0px 33px -20px #000000;
    }

    .orientation-select img {
        cursor: pointer;
        height: 70px;
        width: auto;
        transition: .2s ease-in-out;
    }

    p {
        color: white;
    }

    .size-select > * {
        cursor: pointer;
        color: black;
        background-color: white;
        text-align: center;
        margin: 5px 0;
    }

    .credit {
        position: absolute;
        bottom: 10px;
        width: 100%;
        text-align: center;
    }
</style>