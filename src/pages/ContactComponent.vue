<template>
    <h1>Contact Us</h1>
    <div v-if="success" class="alert alert-success text-start" role="alert">
        Message sent with success!
    </div>
    <div class="row">
        <form class="col-12 text-start" @submit.prevent="sendForm( )" novalidate >
            <div class="mb-3">
                <label for="name" class="form-label">Name</label>
                <input type="text" v-model="name" :class="{'is-invalid': errors.name}" class="form-control border-0 border-bottom" id="name" placeholder="Enter your name" required>  
                <p v-for="(error, index) in errors.name" :key="`message-error-${index}`" class="invalid-feedback">
                    {{ error }}
                </p> 
                
            </div>
            <div class="mb-3">
                <label for="email" class="form-label"></label>
                <input type="email" v-model="address" :class="{ 'is-invalid': errors.address }" class="form-control border-0 border-bottom" id="email" placeholder="Enter your email" required>
                <p v-for="(error, index) in errors.address" :key="`message-error-${index}`" class="invalid-feedback">
                    {{ error }}
                </p>
            </div>
            <div class="mb-3">
                <label for="message" class="form-label">Message</label>
                <textarea :class="{ 'is-invalid': errors.message }" class="form-control border-0 border-bottom" v-model="message" id="message" placeholder="Enter your message" required>{{  message }}</textarea>
                <p v-for="(error, index) in errors.message" :key="`message-error-${index}`" class="invalid-feedback">
                    {{ error }}
                </p>
            </div>
            <button type="submit" :disabled="loading" class="btn btn-success mt-3">{{ loading ? 'Sending...' : 'Send Message' }}</button>
        </form>
    </div>
</template>

<script>
import { store } from '../store';
import axios from 'axios';

export default {
    name: 'ContactComponent',
    data() {
        return {
            store,
            name: '',
            address: '',
            message: '',
            errors: {},
            loading: false,
            success: false
        }
    },
    methods: {
        sendForm() {
            this.success = false;
            this.loading = true;
            this.errors = {};
            const data = {
                name: this.name,
                address: this.address,
                message: this.message
            }
            console.log(data);
            axios.post(`${this.store.apiBaseUrl}/contacts`, data).then((res) => {
                console.log(res.data);
                this.success = true;
                this.name = '';
                this.address = '';
                this.message = '';
            }).catch(error => {
                // console.log(error.response.data);
                this.errors = error.response.data.errors;
                // console.log(this.error);
            }).finally(() => {
                this.loading = false;
            });
        }
    }
}
</script>

<style lang="scss" scoped></style>