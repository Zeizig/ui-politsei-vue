<template>
    <step title="Süüteost teatamise avaldus">

        <card-section>

            <p><strong>Kui kellegi elu või tervis on vahetult ohus, siis helista viivitamatult hädaabinumbrile 112.</strong></p>

            <p>Raskest ja/või isikuvastasest kuriteost teada andmiseks pöördu lähimasse politseijaoskonda.</p>

            <p>Avalduses ei tohi esitada valeandmeid.</p>

            <p>Vajadusel tuleb menetleja kutsel tulla politseijaoskonda täiendavate ütluste andmiseks.</p>

            <p>Tärniga (<span class="required"></span>) tähistatud väljad on kohustuslikud.</p>

        </card-section>

        <card-section class="text-center">

            <h4 class="card-title">Sisene ID-kaardiga</h4>
            <p>ID-kaardiga sisenedes täidetakse automaatselt Sinu isikuandmete väljad</p>

            <a href="#" class="id-card-btn" @click.prevent="onIdCardLoginClicked">
                <img src="static/id-kaart-logo-uus.png" alt="Logi sisse ID-kaardiga">
            </a>
            <a href="#" class="id-card-btn" @click.prevent="onIdCardLoginClicked">
                <img src="static/mid-logo-uus.png" alt="Logi sisse mobiil-IDga">
            </a>

        </card-section>

        <modal :active="modalShowing"
               @confirmed="onIdCardLogin"
               @closed="modalShowing = false">

            <template slot="title">
                Logi sisse ID kaardiga
            </template>

            ID kaardiga sisse logimise mock värk!
        </modal>

    </step>
</template>

<script>
    import Step from './Step.vue';
    import CardSection from '../components/CardSection.vue';
    import Modal from '../components/bootstrap/Modal.vue';

    import StepGenericMixin from '../classes/mixins/stepGeneric';
    import StepMixin from '../classes/mixins/step';

    export default {

        mixins: [ StepGenericMixin, StepMixin ],

        components: { Step, CardSection, Modal },

        props: {
            form: { required: true },
        },

        data() {
            return {
                this_step: 'intro',
                previous_step: '',
                next_step: 'person_data',
                modalShowing: false
            };
        },

        methods: {
            onIdCardLoginClicked() {
                this.modalShowing = true;
            },

            onIdCardLogin() {
                this.modalShowing = false;
                this.form.loggedInWithIdCard();
                setTimeout(() => {
                    this.$router.push('person_data');
                }, 300);
            }
        },

        beforeRouteLeave (to, from, next) {

            if (this.checkErrors(to, from)) {
                return next(false);
            }

            return next();
        }
    }
</script>
