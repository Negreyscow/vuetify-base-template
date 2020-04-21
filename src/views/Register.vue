<template>
    <v-container>
        <v-row>
            <v-col>
                <v-form ref="registerForm" v-model="formValidity">
                    <v-text-field label="Email" type="email" v-model="email" :rules="emailRules" required/>
                    <v-autocomplete 
                        label="Which browser do you use?"
                        :items="browsers"
                    />
                    <v-file-input label="Attach profile picture" />
                    <v-text-field label="Birthday" v-model="birthday" readonly />
                    <v-date-picker v-model="birthday" />
                    <v-checkbox v-model="agreeToTerms" label="Agree to terms & conditions" :rules="agreeToTermsRules" required />
                    <v-btn class="mr-4" type="submit" color="primary" :disabled="!formValidity"> Submit </v-btn>
                    <v-btn class="mr-4" color="success" @click="validateForm">Validate form</v-btn>
                    <v-btn class="mr-4" color="warning" @click="resetValidation">Reset Validation</v-btn>
                    <v-btn class="mr-4" color="error" @click="reset">Reset</v-btn>
                </v-form>
            </v-col>
        </v-row>
    </v-container>  
</template>

<script>
export default {
    data(){
        return {
            birthday: '',
            email: '',
            browsers: ['Chrome', 'Firefox', 'Safari', 'Edge', 'Brave'],
            agreeToTerms: false,
            formValidity: false,

            agreeToTermsRules: [
                value => !!value || 'You must agree!!! :('
            ],
            emailRules: [
                value => !!value || 'Email required',
                value => value.indexOf('@') !== 0 || 'Email should have a username',
                value => value.includes('@') || 'Email invalid format',
                value => value.indexOf('.') - value.indexOf('@') > 1 || 'Invalid domain',
                value => value.indexOf('.') <= value.length - 3 || 'Invalid domain extension'
            ]
        }
    },

    methods: {
        resetValidation(){
            this.$refs.registerForm.resetValidation()
        },

        reset(){
            this.$refs.registerForm.reset()
        },

        validateForm(){
            this.$refs.registerForm.validate()
        }
    }
}
</script>

<style>

</style>