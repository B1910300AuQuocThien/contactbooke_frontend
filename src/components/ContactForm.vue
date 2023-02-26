<template>
    <Form @submit="submitContact" :validation-schema="contactFormschema">
        <div class="form-group">
            <label for="name">Ten</label>
            <Field name="name" type="text" class="form-control" v-model="contactLocal.name" />
            <ErrorMessage name="name" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="email">Email</label>
            <Field name="email" type="email" class="form-control" v-model="contactLocal.email" />
            <ErrorMessage name="email" class="form-feedback" />
        </div>
        <div class="form-group">
            <label for="address">
                Địa chỉ
            </label>
            <Field name="address" type="text" class="form-control" v-model="contactLocal.address" />
            <ErrorMessage name="address" class="form-feedback" />
        </div>
        <div class="form-group">
            <label for="phone">
                Số điện thoại
            </label>
            <Field name="phonr" type="tel" class="form-control" v-model="contactLocal.phone" />
            <ErrorMessage name="phone" class="form-feedback" />
        </div>
        <div class="form-group form-check">
            <input type="checkbox" name="favorite" class="form-check-input" v-model="contactLocal.favorite">
            <label for="favorite" class="form-check-label">
                <strong>Lien he yeu thich</strong>
            </label>
        </div>
        <div class="form-group">
            <button class="btn btn-primary">luu</button>
            <button v-if="contactLocal._id" type="button" class="ml-2 btn btn-danger" @click="deleteContact">
                Xoa
            </button>
        </div>
    </Form>
</template>
<script>
import * as yub from "yup"
import { Form, Field, ErrorMessage } from "vee-validate"
export default {
    components: {
        Form, Field, ErrorMessage
    },
    emits: ["submit:contact", "delete:contact"],
    props: {
        contact: { type: Object, require: true }
    },
    data() {
        const contactFormschema = yub.object().shape({
            name: yub
                .string()
                .required("Tên phải có giá trị")
                .min(2, "Tên phải có ít nhất 2 kí tự")
                .max(50, "Tên có tối đa 50 kí tự"),

            email: yub
                .string()
                .email("Email không đúng")
                .max(50, "Email tối đa 50 kí tự"),
            address: yub.string().max(100, "Địa chỉ tối đa 100 kí tự"),
            phone: yub
                .string()
                .matches(/((09|03|07|08|05)+([0-9]{8})\b)/g, "Số điện thoại không hợp lệ"),
        })
        return {
            contactLocal: this.contact, contactFormschema,
        }
    },
    methods: {
        submitContact() {
            this.$emit("submit:contact", this.contactLocal)
        },
        deleteContact() {
            this.$emit("delete:contact", this.contactLocal.id)
        }
    }
}
</script>
<style scoped>
@import "@/assets/form.css"
</style>