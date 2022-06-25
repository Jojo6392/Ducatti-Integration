<template>
    <div id="app">
        <div class="menu">
        <div class="menu__hamburger">
            <div class="bar"></div>
            <div class="bar"></div>
            <div class="bar"></div>
        </div>
        <div class="menu__liens">
            <img src="./assets/world_icon.png" alt="world icon">
            <div class="border-right">INTERNATIONAL WEBSITE</div>
            <div>MY DUCATI</div>
        </div>
    </div>
    <div class="content">
        <div class="content__title">
            <img src="./assets/logo_ducati.png" alt="ducati logo" style="width: 100px;">
            <img src="./assets/monster_text.png" alt="monster text" style="width: 250px;">
        </div>
        <div class="content__desc">
            <!-- moto 1 -->
            <div class="moto" v-for="(moto, i) in motos" :key="i" :class="{init: i !== 0 && initFinished !== true}">
                <div class="desc__numero" :class="{hiddenNumero: !moto.isActive, activeNumero: i === index}">{{ moto.numero }}</div>
                <img class="desc__img" :src="moto.image" :class="{hiddenMoto: !moto.isActive, activeMoto: i === index}">
            </div>
            <div class="white_frame">
                <div class="white_frame_desc" v-if="index == 0 || index == 2">
                    <div class="text_desc">Displacement</div>
                    <div class="text_score">803 cc</div>
                    <div class="text_desc">Horse Power</div>
                    <div class="text_score">73 hp (54 kW)</div>
                    <div class="text_desc">Torque</div>
                    <div class="text_score">67 Nm (49.0 lb-ft)</div>
                    <div class="text_desc">Dry Weight</div>
                    <div class="text_score">175 Kg (386 lb)</div>
                    <div class="text_desc">Seat Height</div>
                    <div class="text_score">805 mm (31.69 in)</div>
                    <div class="text_desc">Safety</div>
                    <div class="text_score">ABS</div>
                </div>
                <div class="white_frame_desc" v-else>
                    <div class="text_desc">Displacement</div>
                    <div class="text_score">821 cc</div>
                    <div class="text_desc">Horse Power</div>
                    <div class="text_score">109 hp (80 kW)</div>
                    <div class="text_desc">Torque</div>
                    <div class="text_score">86 Nm (63 lb-ft)</div>
                    <div class="text_desc">Dry Weight</div>
                    <div class="text_score">180.5 Kg (398 lb)</div>
                    <div class="text_desc">Seat Height</div>
                    <div class="text_score">805 mm (31.69 in)</div>
                    <div class="text_desc">Safety</div>
                    <div class="text_score">ABS</div>
                </div>
                <div class="white_frame_color">
                    <div class="block red" style="background: #DF1F26;" :class="{active_block: index === 0, not_active_block: index !== 0}" @click="changeItemBlock(0)"></div>
                    <div class="block black" style="background: #141414;" :class="{active_block: index === 1, not_active_block: index !== 1}" @click="changeItemBlock(1)"></div>
                    <div class="block gray" style="background: #E4E4E4;" :class="{active_block: index === 2, not_active_block: index !== 2}" @click="changeItemBlock(2)"></div>
                </div>
                <div class="white_frame_text">
                    <div>Fresh vibes.</div>
                    <div style="margin-left: 100px;">Sporty soul.</div>
                </div>
            </div>
        </div>
    </div>
    <img class="arrow arrow-left" src="./assets/left_arrow.png" alt="left arrow" @click="changeItem(false)">
    <img class="arrow arrow-right" src="./assets/right_arrow.png" alt="right arrow" @click="changeItem(true)">
    </div>
</template>

<script>

export default {
    name: 'App',

    data() {
        return {
            index: 0,
            initFinished: false,
            motos : [
                {
                    image: require("./assets/Monster-797.png"),
                    numero: "797",
                    isActive: true
                },
                {
                    image: require("./assets/Monster-821.png"),
                    numero: "821",
                    isActive: false
                },
                {
                    image: require("./assets/Monster-999.png"),
                    numero: "999",
                    isActive: false
                },
            ]
        }
    },

    mounted() {
        setTimeout(() => {
            this.initFinished = true
        }, 500)
    },

    methods: {
        changeItem: function(isRight) {
            const nbItems = this.motos.length

            if(isRight) {
                if(this.index + 1 < nbItems) {
                    this.motos[this.index].isActive = false
                    this.index += 1
                    this.motos[this.index].isActive = true
                }
            }

            else {
                if(this.index != 0) {
                    this.motos[this.index].isActive = false
                    this.index -= 1
                    this.motos[this.index].isActive = true
                }
            }
        },

        changeItemBlock: function(indexItem) {

            this.motos[this.index].isActive = false
            if(indexItem === 0) this.index = 0
            else if(indexItem === 1) this.index = 1
            else this.index = 2
            this.motos[this.index].isActive = true
        }
    }
}
</script>

<style scoped>
#app {
    width: 100%;
    height: 100%;
}
.arrow {
    position: absolute;
    top: 40%;
    cursor: pointer;
}

.arrow-right {
    right: 15%;
}

.arrow-left {
    left: 15%;
}

.init {
    opacity: 0;
}

/* MENU SECTION */

.menu {
    width: 100%;
    height: 15%;
    display: flex;
    align-items: center;
}

.menu__hamburger {
    padding-left: 10%;
    width: 50%;
    display: flex;
    flex-direction: column;
}

.bar {
    border: 1px solid white;
    width: 25px;
    margin-bottom: 7px;
}

.menu__liens {
    width: 50%;
    padding-right: 10%;
    justify-content: end;
    display: flex;
    align-items: center;
    gap: 20px;
    font-size: 14px;
}

.border-right {
    border-right: 1px solid white;
    padding-right: 20px;
}

/* CONTENT SECTION */

.content {
    flex-direction: column;
    height: 85%;
    transform: translateY(-10%);
    width: 100%;
    position: relative;
}

.activeMoto {
    animation: activeMoto 250ms forwards;
    animation-delay: 500ms; 
}

.activeNumero {
    animation: activeNumero 250ms forwards;
    animation-delay: 350ms; 
}

@keyframes activeMoto {
    from {
        transform: translate(100%, -10%);
        opacity: 0;
        display: none;
    }
    to {
        transform: translate(0%, -10%);
        opacity: 1;
        display: block;
    }
    
}

@keyframes activeNumero {
    from {
        transform: translate(100%, 65%);
        opacity: 0;
        display: none;
    }
    to {
        transform: translate(0%, 65%);
        opacity: 1;
        display: block;
    }
    
}

.hiddenMoto {
    animation: hiddenMoto 250ms forwards;
}

.hiddenNumero {
    animation: hiddenNumero 250ms forwards;
    animation-delay: 100ms;
}

@keyframes hiddenMoto {
    from {
        transform: translate(0, -10%);
        opacity: 1;
        display: block;
    }
    to {
        transform: translate(-100%, -10%);
        opacity: 0;
        display: none;
    }
    
}

@keyframes hiddenNumero {
    from {
        transform: translate(0, 65%);
        opacity: 1;
        display: block;
    }
    to {
        transform: translate(-100%, 65%);
        opacity: 0;
        display: none;
    }
    
}

.moto {
    z-index: 2;
    text-align: center;
    position: absolute;
}

.content img {
    width: min-content;
}

.content__title {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.content__title img {
    margin-bottom: 30px;
}

.content__desc {
    display: flex;
    position: absolute;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.content__desc img {
    width: 788px;
    height: 488px;
    transform: translateY(-10%);
}

.desc__numero {
    font-family: 'Lato Black';
    font-size: 150px;
    transform: translateY(65%);
    opacity: 0;
}

.desc__img {
    opacity: 0;
}

.white_frame {
    display: flex;
    align-items: flex-end;
    background: #FFFFFF;
    box-shadow: 0px 40px 30px rgba(60, 49, 13, 0.15);
    border-radius: 50px;
    width: 80%;
    transform: translateY(80%);
    color: black;
}

.white_frame_desc, .white_frame_color, .white_frame_text {
    width: 33%;
    color: #181818;
    padding-left: 4em;
    padding-top: 2em;
    padding-bottom: 1em;
}

.text_desc {
    font-size: 14px;
    font-weight: 300;
}

.text_score {
    font-size: 24px;
    font-weight: 900;
    letter-spacing: 0.095em;
    margin-bottom: 10px;
}

.white_frame_color {
    display: flex;
    gap: 50px;
    margin-bottom: 30px;
}

.white_frame_text {
    font-family: 'Italianno';
    font-size: 50px;
    color: #707070;
    letter-spacing: 0.135em;
    font-weight: 400;
    padding-bottom: 50px;
    padding-left: 0;
}

.block {
    border-radius: 16px;
    width: 90px;
    height: 90px;
    z-index: 3;
    cursor: pointer;
}

.active_block {
    filter: drop-shadow(0px 4px 32px rgba(0, 0, 0, 0.6));
    transform: scale(1.15);
    animation: activeBlock 1s forwards;
}

.not_active_block {
    filter: drop-shadow(0px 4px 32px rgba(0, 0, 0, 0.6));
    transform: scale(1.15);
    animation: notActiveBlock 1s forwards;
}

@keyframes activeBlock {
    from {
        transform: scale(1);
        filter: drop-shadow(0px 4px 32px rgba(0, 0, 0, 0.6));
    }
    to {
        filter: drop-shadow(0px 4px 32px rgba(0, 0, 0, 0.6));
        transform: scale(1.15);
    }
}

@keyframes notActiveBlock {
    from {
        filter: drop-shadow(0px 4px 32px rgba(0, 0, 0, 0.6));
        transform: scale(1.15);
    }
    to {
        filter: none;
        transform: scale(1);
    }
}

</style>
