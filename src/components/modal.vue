<style scoped>
    .modal-backdrop {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        box-sizing: border-box;
        padding-left: 95px;
        position: relative;
        width: 900px;
        height: 600px;
        background: #FFFFFF;
        box-shadow: 2px 2px 20px 1px;
        overflow-x: auto;
        animation-duration: .2s;
        animation-name: appearin;
    }

    .modal__close {
        position: absolute;
        top: 19px;
        right: 19px;
        cursor: pointer;
    }

    .modal__header .modal__step {
        margin: 0;
        margin-bottom: 20px;
        padding-top: 110px;
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 500;
        font-size: 100px;
        line-height: 90px;
        color: #0DE7EF;
    }

    .modal__header .modal__title {
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 500;
        font-size: 48px;
        line-height: 56px;
        color: #00263E;
    }

    .modal__divider {
        margin-top: 20px;
        width: 96px;
        height: 1px;
        background: #00263E;
    }

    .modal__body {
        max-width: 646px;
        margin-top: 24px;
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size: 18px;
        line-height: 30px;
        color: #727272;
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
        .modal {
            max-width: 630px;
            padding: 0 4rem 0 4rem;
        }

        .modal__container {
            width: max-content;
            margin: auto;
        }

        .modal__header .modal__step {
            margin-bottom: 0;
            font-size: 70px;
            line-height: 70px;
        }

        .modal__header .modal__title {
            font-size: 38px;
            line-height: 46px;
        }

        .modal__body {
            max-width: fit-content;
        }
    }

    @media screen and (max-width: 767px) {
        .modal {
            height: auto;
            margin-left: 2rem;
            margin-right: 2rem;
            padding: 0 3rem 3rem 3rem;
        }

        .modal__container {
            width: auto;
        }

        .modal__header .modal__step {
            padding-top: 50px;
            font-size: 40px;
            line-height: 40px;
        }

        .modal__header .modal__title {
            font-size: 24px;
        }

        .modal__body {
            font-size: 1rem;
        }

        .modal__close {
            height: 25px;
        }
    }

</style>
<template>
  <div class="modal-backdrop">
    <div class="modal">
        <img @click="$emit('close-modal')" class="modal__close" src="../assets/Group.svg" alt="Close Button">
        <div class="modal__container">
            <header class="modal__header">
                <h1 v-if="stepNumber" class="modal__step">
                    {{stepNumber}}
                </h1>
                <div class="modal__title">
                    <slot name="header">
                    </slot>
                </div>
            </header>  

            <div class="modal__divider" />

            <section class="modal__body">
                <slot name="body">
                </slot>
            </section>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        stepNumber: {
            type: String,
            required: false
        }
    }
}
</script>