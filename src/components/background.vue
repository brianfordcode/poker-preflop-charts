<template>
  <div class="background">
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
   <span></span>
</div>
</template>

<style scoped>
@keyframes move {
    100% {
        transform: translate3d(0, 0, 1px) rotate(360deg);
    }
}

.background {
    position: absolute;
    z-index: -1000;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    background: #1a4422;
    overflow: hidden;
}

.background span {
    width: 30vmin;
    height: 30vmin;
    border-radius: 30vmin;
    backface-visibility: hidden;
    position: absolute;
    animation: move;
    animation-duration: 5;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
    opacity: 0.75;
}


.background span:nth-child(0) {
    color: #0f0b50;
    top: 39%;
    left: 93%;
    animation-duration: 300s;
    animation-delay: -99s;
    transform-origin: -3vw -14vh;
    box-shadow: 60vmin 0 8.315077130925845vmin currentColor;
}
.background span:nth-child(1) {
    color: #0f0b50;
    top: 26%;
    left: 90%;
    animation-duration: 401s;
    animation-delay: -71s;
    transform-origin: 25vw -5vh;
    box-shadow: 60vmin 0 7.5014799353938635vmin currentColor;
}
.background span:nth-child(2) {
    color: #858585;
    top: 23%;
    left: 35%;
    animation-duration: 206s;
    animation-delay: -304s;
    transform-origin: -12vw -7vh;
    box-shadow: 60vmin 0 7.978277810903238vmin currentColor;
}
.background span:nth-child(3) {
    color: #0f0b50;
    top: 47%;
    left: 37%;
    animation-duration: 300s;
    animation-delay: -117s;
    transform-origin: 5vw 7vh;
    box-shadow: 60vmin 0 8.184596372221069vmin currentColor;
}
.background span:nth-child(4) {
    color: #c20505;
    top: 93%;
    left: 68%;
    animation-duration: 200s;
    animation-delay: -12s;
    transform-origin: -11vw 7vh;
    box-shadow: -60vmin 0 7.9937659028138786vmin currentColor;
}
.background span:nth-child(5) {
    color: #0f0b50;
    top: 65%;
    left: 98%;
    animation-duration: 184s;
    animation-delay: -124s;
    transform-origin: 7vw -19vh;
    box-shadow: 60vmin 0 7.724128427238561vmin currentColor;
}
.background span:nth-child(6) {
    color: #0f0b50;
    top: 30%;
    left: 82%;
    animation-duration: 403s;
    animation-delay: -74s;
    transform-origin: 11vw -5vh;
    box-shadow: 60vmin 0 7.530040838818497vmin currentColor;
}
.background span:nth-child(7) {
    color: #c20505;
    top: 75%;
    left: 45%;
    animation-duration: 297s;
    animation-delay: -422s;
    transform-origin: -3vw -13vh;
    box-shadow: 60vmin 0 7.5009669464958035vmin currentColor;
}
.background span:nth-child(8) {
    color: #0f0b50;
    top: 5%;
    left: 6%;
    animation-duration: 441s;
    animation-delay: -193s;
    transform-origin: 13vw -23vh;
    box-shadow: -60vmin 0 7.659805879291114vmin currentColor;
}
.background span:nth-child(9) {
    color: #1f1f1f;
    top: 92%;
    left: 11%;
    animation-duration: 134s;
    animation-delay: -23s;
    transform-origin: -21vw -11vh;
    box-shadow: -60vmin 0 7.714571880644323vmin currentColor;
}
.background span:nth-child(10) {
    color: #c20505;
    top: 41%;
    left: 30%;
    animation-duration: 170s;
    animation-delay: -166s;
    transform-origin: 4vw 18vh;
    box-shadow: -60vmin 0 7.951564099960101vmin currentColor;
}
.background span:nth-child(11) {
    color: #181818;
    top: 62%;
    left: 78%;
    animation-duration: 117s;
    animation-delay: -421s;
    transform-origin: -20vw -23vh;
    box-shadow: 60vmin 0 7.7671164676143984vmin currentColor;
}
.background span:nth-child(12) {
    color: #0f0b50;
    top: 45%;
    left: 47%;
    animation-duration: 204s;
    animation-delay: -100s;
    transform-origin: -2vw 0vh;
    box-shadow: 60vmin 0 7.597093472446534vmin currentColor;
}
.background span:nth-child(13) {
    color: #c20505;
    top: 34%;
    left: 59%;
    animation-duration: 400s;
    animation-delay: -16s;
    transform-origin: -16vw -2vh;
    box-shadow: -60vmin 0 8.44257517777871vmin currentColor;
}
.background span:nth-child(14) {
    color: #858585;
    top: 49%;
    left: 24%;
    animation-duration: 442s;
    animation-delay: -152s;
    transform-origin: -6vw -7vh;
    box-shadow: -60vmin 0 8.32566784830023vmin currentColor;
}
.background span:nth-child(15) {
    color: #141414;
    top: 60%;
    left: 76%;
    animation-duration: 303s;
    animation-delay: -447s;
    transform-origin: -10vw 16vh;
    box-shadow: 60vmin 0 7.548396418811129vmin currentColor;
}
.background span:nth-child(16) {
    color: #0f0b50;
    top: 65%;
    left: 50%;
    animation-duration: 300s;
    animation-delay: -309s;
    transform-origin: -3vw -23vh;
    box-shadow: -60vmin 0 8.261910277170163vmin currentColor;
}
.background span:nth-child(17) {
    color: #c20505;
    top: 70%;
    left: 17%;
    animation-duration: 226s;
    animation-delay: -349s;
    transform-origin: -7vw -11vh;
    box-shadow: 60vmin 0 8.456627837546385vmin currentColor;
}
.background span:nth-child(18) {
    color: #0f0b50;
    top: 90%;
    left: 15%;
    animation-duration: 166s;
    animation-delay: -345s;
    transform-origin: 2vw -2vh;
    box-shadow: -60vmin 0 7.508110278156867vmin currentColor;
}
.background span:nth-child(19) {
    color: #c20505;
    top: 50%;
    left: 65%;
    animation-duration: 367s;
    animation-delay: -311s;
    transform-origin: 3vw 14vh;
    box-shadow: 60vmin 0 8.423183517593182vmin currentColor;
}
.background span:nth-child(20) {
    color: #131313;
    top: 20%;
    left: 90%;
    animation-duration: 300s;
    animation-delay: -294s;
    transform-origin: -13vw 6vh;
    box-shadow: 60vmin 0 7.723704409368295vmin currentColor;
}
.background span:nth-child(21) {
    color: #858585;
    top: 48%;
    left: 72%;
    animation-duration: 280s;
    animation-delay: -137s;
    transform-origin: -9vw 11vh;
    box-shadow: 60vmin 0 7.818921884383295vmin currentColor;
}
.background span:nth-child(22) {
    color: #0f0b50;
    top: 56%;
    left: 35%;
    animation-duration: 306s;
    animation-delay: -275s;
    transform-origin: 21vw 11vh;
    box-shadow: -60vmin 0 8.282098840620723vmin currentColor;
}
.background span:nth-child(23) {
    color: #c20505;
    top: 99%;
    left: 87%;
    animation-duration: 333s;
    animation-delay: -408s;
    transform-origin: 5vw 7vh;
    box-shadow: -60vmin 0 7.772670180732542vmin currentColor;
}
.background span:nth-child(24) {
    color: #858585;
    top: 53%;
    left: 9%;
    animation-duration: 167s;
    animation-delay: -231s;
    transform-origin: -17vw -18vh;
    box-shadow: -60vmin 0 7.540325187538355vmin currentColor;
}
.background span:nth-child(25) {
    color: #858585;
    top: 23%;
    left: 14%;
    animation-duration: 163s;
    animation-delay: -30s;
    transform-origin: -13vw 3vh;
    box-shadow: 60vmin 0 8.488000906700455vmin currentColor;
}
.background span:nth-child(26) {
    color: #858585;
    top: 82%;
    left: 7%;
    animation-duration: 176s;
    animation-delay: -287s;
    transform-origin: -24vw 2vh;
    box-shadow: -60vmin 0 7.674985011467724vmin currentColor;
}
.background span:nth-child(27) {
    color: #c20505;
    top: 16%;
    left: 60%;
    animation-duration: 104s;
    animation-delay: -57s;
    transform-origin: -9vw 7vh;
    box-shadow: -60vmin 0 7.610309714075097vmin currentColor;
}
.background span:nth-child(28) {
    color: #0f0b50;
    top: 43%;
    left: 60%;
    animation-duration: 180s;
    animation-delay: -75s;
    transform-origin: -5vw 2vh;
    box-shadow: 60vmin 0 8.391222722120851vmin currentColor;
}
.background span:nth-child(29) {
    color: #0f0b50;
    top: 74%;
    left: 30%;
    animation-duration: 146s;
    animation-delay: -439s;
    transform-origin: 5vw -4vh;
    box-shadow: -60vmin 0 7.706323837418921vmin currentColor;
}
.background span:nth-child(30) {
    color: #1d1d1d;
    top: 55%;
    left: 10%;
    animation-duration: 403s;
    animation-delay: -278s;
    transform-origin: 22vw -5vh;
    box-shadow: 60vmin 0 8.150335812804524vmin currentColor;
}
.background span:nth-child(31) {
    color: #858585;
    top: 10%;
    left: 54%;
    animation-duration: 204s;
    animation-delay: -66s;
    transform-origin: -23vw -1vh;
    box-shadow: -60vmin 0 8.06669805980908vmin currentColor;
}
.background span:nth-child(32) {
    color: #c20505;
    top: 92%;
    left: 56%;
    animation-duration: 282s;
    animation-delay: -187s;
    transform-origin: 10vw 20vh;
    box-shadow: -60vmin 0 7.67088001908694vmin currentColor;
}
.background span:nth-child(33) {
    color: #c20505;
    top: 41%;
    left: 42%;
    animation-duration: 181s;
    animation-delay: -284s;
    transform-origin: 0vw -10vh;
    box-shadow: -60vmin 0 7.809307513286785vmin currentColor;
}
.background span:nth-child(34) {
    color: #1b1b1b;
    top: 62%;
    left: 10%;
    animation-duration: 367s;
    animation-delay: -218s;
    transform-origin: 2vw 10vh;
    box-shadow: 60vmin 0 7.731966496362997vmin currentColor;
}
.background span:nth-child(35) {
    color: #0f0b50;
    top: 43%;
    left: 7%;
    animation-duration: 419s;
    animation-delay: -358s;
    transform-origin: -21vw -3vh;
    box-shadow: 60vmin 0 8.049931584040872vmin currentColor;
}
.background span:nth-child(36) {
    color: #131313;
    top: 10%;
    left: 89%;
    animation-duration: 237s;
    animation-delay: -36s;
    transform-origin: -7vw 16vh;
    box-shadow: 60vmin 0 7.796582193781825vmin currentColor;
}
.background span:nth-child(37) {
    color: #0f0b50;
    top: 49%;
    left: 3%;
    animation-duration: 352s;
    animation-delay: -74s;
    transform-origin: -16vw -14vh;
    box-shadow: -60vmin 0 8.439162958605325vmin currentColor;
}
.background span:nth-child(38) {
    color: #858585;
    top: 44%;
    left: 65%;
    animation-duration: 146s;
    animation-delay: -186s;
    transform-origin: 3vw 13vh;
    box-shadow: 60vmin 0 8.392877183394857vmin currentColor;
}
.background span:nth-child(39) {
    color: #0f0b50;
    top: 5%;
    left: 30%;
    animation-duration: 300s;
    animation-delay: -264s;
    transform-origin: 12vw -12vh;
    box-shadow: -60vmin 0 7.795348011784247vmin currentColor;
}
.background span:nth-child(40) {
    color: #858585;
    top: 29%;
    left: 76%;
    animation-duration: 333s;
    animation-delay: -432s;
    transform-origin: -13vw 4vh;
    box-shadow: 60vmin 0 7.901037786670942vmin currentColor;
}
.background span:nth-child(41) {
    color: #c20505;
    top: 42%;
    left: 27%;
    animation-duration: 88s;
    animation-delay: -296s;
    transform-origin: -22vw 21vh;
    box-shadow: -60vmin 0 7.729865773252483vmin currentColor;
}
.background span:nth-child(42) {
    color: #0f0b50;
    top: 30%;
    left: 25%;
    animation-duration: 216s;
    animation-delay: -160s;
    transform-origin: 1vw -9vh;
    box-shadow: 60vmin 0 8.15938212772266vmin currentColor;
}
.background span:nth-child(43) {
    color: #0f0b50;
    top: 92%;
    left: 79%;
    animation-duration: 233s;
    animation-delay: -229s;
    transform-origin: 10vw -15vh;
    box-shadow: -60vmin 0 8.17576243750801vmin currentColor;
}
.background span:nth-child(44) {
    color: #858585;
    top: 41%;
    left: 81%;
    animation-duration: 51s;
    animation-delay: -203s;
    transform-origin: -18vw 3vh;
    box-shadow: 60vmin 0 7.611907924548271vmin currentColor;
}
.background span:nth-child(45) {
    color: #161616;
    top: 13%;
    left: 64%;
    animation-duration: 449s;
    animation-delay: -313s;
    transform-origin: -21vw 22vh;
    box-shadow: -60vmin 0 8.02885490347144vmin currentColor;
}
.background span:nth-child(46) {
    color: #0f0b50;
    top: 79%;
    left: 30%;
    animation-duration: 301s;
    animation-delay: -6s;
    transform-origin: -11vw -7vh;
    box-shadow: 60vmin 0 7.802830019923579vmin currentColor;
}
.background span:nth-child(47) {
    color: #858585;
    top: 26%;
    left: 22%;
    animation-duration: 254s;
    animation-delay: -254s;
    transform-origin: -18vw -18vh;
    box-shadow: -60vmin 0 7.576935418907948vmin currentColor;
}
.background span:nth-child(48) {
    color: #0f0b50;
    top: 61%;
    left: 78%;
    animation-duration: 433s;
    animation-delay: -409s;
    transform-origin: 9vw 3vh;
    box-shadow: 60vmin 0 7.7708724001682vmin currentColor;
}
.background span:nth-child(49) {
    color: #0f0b50;
    top: 7%;
    left: 8%;
    animation-duration: 455s;
    animation-delay: -386s;
    transform-origin: 11vw -13vh;
    box-shadow: 60vmin 0 8.116291770204088vmin currentColor;
}
</style>