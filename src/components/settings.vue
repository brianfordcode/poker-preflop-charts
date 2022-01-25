<template>

<div class="container">
    <img
        src="../assets/settings-gear.png"
        alt="gear-icon"
        @click="showModal = !showModal"
        draggable="false"
    />

    <div
        class="box"
        v-if="showModal"
    >
        <div style="display:flex; align-items: center; margin-top: 30px">
            <p>Background:</p>
            <input type="color">
        </div>

        <p class="credit">Created by: <a href="https://www.brianfordcode.com" target="_blank">Brian Ford</a></p>

    </div>
</div>



</template>

<script>
export default {
    data() {
        return {
            showModal: false,
        }
    }
// @mouseleave="showModal = false"
}
</script>

<style scoped>

.container {
    z-index: 10000;
}

img {
    position: absolute;
    height: 25px;
    right: 0;
    margin: 20px;
    transition: 1s ease-in-out;
    cursor: pointer;
}

img:hover {
    transform: rotate(180deg);
}

.box {
    position: absolute;
    display: flex;
    justify-content: space-around;
    align-items: flex-start;
    right: 20px;
    top: 50px;
    height: 250px;
    width: 200px;
    background-color: rgba(0,0,0,0.95);
    box-shadow: 0px 0px 33px -20px #000000;
}

p {
    color: white;
}

input {
    border: none;
    outline: none;
}

.credit {
    position: absolute;
    bottom: 10px;
    width: 100%;
    text-align: center;
}





</style>