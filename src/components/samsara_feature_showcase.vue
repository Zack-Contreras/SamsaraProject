<style scoped>
    .features {
        display: flex;
        margin-top: 145px;
    }

    .features__steps {
        margin-right: 62px;
    }

    .feature__step {
        display: flex;
        font-family: 'Roboto';
        color: white;
        mix-blend-mode: normal;
        opacity: 0.25;
        cursor: pointer;
        transition: all .2s ease-in;
    }

    .feature__step:hover {
        opacity: .5;
    }

    .feature__container.active .feature__step {
        opacity: 1;
    }

    .feature__step h1 {
        margin: 0;
        padding-right: 26px;
        font-style: normal;
        font-weight: 500;
        font-size: 100px;
        line-height: 90px;
    }

    .feature__step p {
        max-width: 15ch;
        margin: 0;
        font-style: normal;
        font-weight: 700;
        font-size: 36px;
        line-height: 42px;
    }

    .features__divider {
        margin-top: 36px;
        margin-bottom: 36px;
        margin-left: 57px;
        width: 2px;
        height: 95px;
        background: white;
        mix-blend-mode: normal;
        opacity: 0.25;
        transition: all .2s ease-in;
    }

    .feature__container.active .features__divider {
        opacity: 1;
    }

    .features__img {
        position: relative;
    }

    .features__img .features__spotlight {
        max-width: 580px;
        height: auto;
        border-radius: 35px;
        transition: all .2s ease-in;
        filter: drop-shadow(10px 10px 4px rgba(0,0,0,.7));
        -webkit-box-shadow:0px 0px 300px 67px rgba(48,153,161,0.55);
        -moz-box-shadow: 0px 0px 300px 67px rgba(48,153,161,0.55);
        box-shadow: 0px 0px 300px 67px rgba(48,153,161,0.55);
    }

    .features__img .features__popup-icon {
        position: absolute;
        cursor: pointer;
        top: 55px;
        right: 55px;
    }

    .v-enter-active,
    .v-leave-active {
        transition: opacity .2s ease;
    }

    .v-enter-from,
    .v-leave-to {
        opacity: 0;
    }

    .features__spotlight--animate {
        animation-duration: .3s;
        animation-name: appearin;
    }

    .features__arrow {
        display: none;
    }

    @keyframes appearin {
        from {
            opacity: 0;

        }

        to {
            opacity: 1;
        }
    }

    @media screen and (max-width: 1224px) {

        .features {
            margin-top: 80px;
        }

        .feature__step h1 {
            font-size: 60px;
            padding-right: 13px;
        }  

        .feature__step p {
            padding-top: 18px;
            font-size: 22px;
            line-height: 26px;
        }

        .features__divider {
            height: 60px;
            margin-top: 16px;
            margin-bottom: 16px;
        }

        .features__img .features__spotlight {
            max-width: 400px;
        }

        .features__img .features__popup-icon {
            height: 60px;
            top: 20px;
            right: 20px;
        }
  }

    @media screen and (max-width: 767px) {
        .features {
            flex-direction: column;
            margin-top: 40px;
        }

        .features__steps {
            display: flex;
            justify-content: center;
            margin-right: 0;
        }

        .feature__container {
            display: none;
        }

        .feature__container.active {
            display: block;
        }

        .features__img {
            display: flex;
            justify-content: center;
            width: fit-content;
            margin: auto;
        }

        .features__divider {
            display: none;
        }

        .features__img .features__spotlight {
            max-width: 300px;
        }

        .features__img .features__popup-icon {
            height: 40px;
            top: 20px;
            right: 20px;
        }

        .features__arrow {
            display: block;
            position: absolute;
            cursor: pointer;
            height: 40px;
            top: 40%;
        }

        .features__arrow.features__arrow--left {
            left: -40px;
            transform: rotate(180deg);
        }

        .features__arrow.features__arrow--right {
            right: -40px;
            
        }
    }
</style>

<template>
    <div class="features">
        <section class="features__steps">
            <div @click="activateStep(i)" v-for="(step,i) in steps" :key="step.step" class="feature__container" :class="{active: step.active}">
                <div class="feature__step">
                    <h1>{{step.step}}</h1>
                    <p>{{step.title}}</p>
                </div>
                <div v-if="i !== steps.length - 1" class="features__divider" />
            </div>
        </section>
        <section class="features__img">
            <img :class="{'features__spotlight--animate': animateImg}" :src="featureImage" :alt="activeStep.title" class="features__spotlight">
            <img @click="openModal" src="../assets/popup_icon.png" alt="popup icon" class="features__popup-icon">
            <img 
                @click="nextStep" 
                v-show="currentIndex !== steps.length - 1" 
                class="features__arrow features__arrow--right" 
                src="../assets/arrow.svg" 
                alt=""
            >
            <img  
                @click="previousStep" 
                v-show="currentIndex !== 0" 
                class="features__arrow features__arrow--left" 
                src="../assets/arrow.svg" 
                alt=""
            >
        </section>
        <!-- Modal for popup content -->
        <Transition>
            <samsara-modal @close-modal="closeModal" v-if="showModal" :stepNumber="activeStep.step">
                <template v-slot:header>
                    {{activeStep.title}}
                </template>

                <template v-slot:body>
                    {{activeStep.popupContent}}
                </template>
            </samsara-modal>
        </Transition>
    </div>
</template>

<script>
import Modal from './modal.vue'
export default {
    data() {
        return {
            animateImg: false,
            showModal: false,
            currentIndex: 0,
            steps: [
                {step: "01", title: "Real-time GPS Tracking", active: true, url: '../assets/step_1.png', popupContent: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip."},
                {step: "02", title: "AI-enabled Safety Cameras", active: false, url: "../assets/step_2.png", popupContent: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip."},
                {step: "03", title: "Routing and Location Sharing", active: false, url: "../assets/step_3.png", popupContent: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip."},
            ]
        }
    },
    components: {
        'samsara-modal': Modal
    },
    computed: {
        activeStep() {
            return this.steps.find((step,i) =>  {
                        this.currentIndex = i
                        return step.active
                    })
        },
        featureImage() {
            return require(`../assets/step_${this.activeStep.step}.png`)
        }
    },
    methods: {
        closeModal() {
            this.showModal = false
        },
        openModal() {
            this.showModal = true
        },
        activateStep(index) {
            if(!this.steps[index].active) this.animateImg = true

            this.steps = this.steps.map((step,i) => {
                if(i === index) {
                    return {
                        ...step,
                        active: true
                    }
                } else {
                    return {
                        ...step,
                        active: false
                    }
                }
            })
            setTimeout(() => {
                this.animateImg = false
            }, 300)
        },
        nextStep() {
            this.activateStep(this.currentIndex + 1)
        },
        previousStep() {
            this.activateStep(this.currentIndex - 1)
        }
    }
}
</script>