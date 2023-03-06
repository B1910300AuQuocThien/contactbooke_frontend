
<template>
    <h1 class="text-center"> Tạo liên hệ</h1>
    <ContactForm @submit:contact="createContact" :contact="contact" class="p-5"></ContactForm>
    <p>{{ message }}</p>
</template>

<script>
import ContactForm from '../components/ContactForm.vue';
import contactService from '../services/contact.service';
export default {
    components: {
        ContactForm
    },

    data() {
        return {
            contact: {},
            message: ""
        }
    },
    methods: {
        async createContact(data) {
            try {
                await contactService.create(data)
                this.message = "Liên hệ được tạo"
            }
            catch (error) {
                console.log(error)
            }
        }
    }
}
</script>

<style></style>