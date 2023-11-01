<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm 
            :contact="contact"
            @submit:contact="addContact"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    props: {},
    data() {
        return {
            contact: {},
            message: ""
        }
    },
    methods: {
        async addContact(data) {
            try {
                this.contact = await ContactService.create(data);
                this.message = "Liên hệ đã được tạo thành công !"

            } catch (err) {
                console.log(err);
            }
        }
    },
    created() {
        this.addContact();
        this.message = "";
    }
}
</script>