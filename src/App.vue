<script setup>
import { reactive } from "vue";
const name = "Bergman";
const socials = [{ icon: "mdi-github", link: "https://github.com/bergmanx" }];
const stackImages = ["python.png", "vue.png", "javascript.png"];
const projects = [];
const parallax = "parallax.png";

const form = reactive({
    name: null,
    email: null,
    email: null,
    _hidden: "",
    loading: false
});

const snackbar = reactive({ active: false, message: null, color: null });

function onSubmit() {
    form.loading = true;
    fetch(import.meta.env.VITE_CONTACTME_URL, {
        method: "POST",
        body: JSON.stringify({
            name: form.name,
            email: form.email,
            message: form.message,
            honeypot: form._hidden
        }),
        headers: { "Content-Type": "application/json" }
    })
        .then(response => {
            if (response.status == 201) {
                return response.json();
            }
            snackbar.message =
                "An error has occurred. Check the form and try again";
            snackbar.color = "red";
            snackbar.active = true;
            form.loading = false;
            return response;
        })
        .then(response => {
            if (response.status == "success") {
                snackbar.message =
                    "Thank you for contact me. I'll write you soon";
                snackbar.color = "success";
                snackbar.active = true;
                form.loading = false;
            }
        });
}

oncontextmenu = () => false;
</script>

<template>
    <v-app>
        <v-parallax :src="parallax">
            <v-system-bar color="primary">
                <span>{{ name }}</span>
                <v-spacer></v-spacer>
                <a
                    v-for="social in socials"
                    :href="social.link"
                    class="text-white"
                >
                    <v-icon :icon="social.icon" class="mr-4"></v-icon>
                </a>
            </v-system-bar>
            <v-container class="text-center mt-8">
                <div class="text-h2">Web Developer</div>
            </v-container>
            <v-container class="mb-4">
                <v-slide-group center-active>
                    <v-slide-group-item v-for="image in projects">
                        <v-img width="250px" :src="image"> </v-img>
                    </v-slide-group-item>
                </v-slide-group>
            </v-container>
            <v-container class="mb-4">
                <v-row justify="center">
                    <v-col cols="auto" v-for="image in stackImages">
                        <v-avatar
                            :image="image"
                            rounded="0"
                            size="60"
                        ></v-avatar>
                    </v-col>
                </v-row>
            </v-container>
            <v-container class="mb-4">
                <v-theme-provider theme="light">
                    <v-form @submit.prevent="onSubmit" :disabled="form.loading">
                        <v-text-field
                            v-model="form.name"
                            name="name"
                            placeholder="Your name"
                            variant="solo"
                            rounded
                        ></v-text-field>
                        <v-text-field
                            v-model="form.email"
                            name="email"
                            type="email"
                            placeholder="Your email"
                            variant="solo"
                            rounded
                        ></v-text-field>
                        <v-textarea
                            v-model="form.message"
                            name="message"
                            placeholder="Message"
                            variant="solo"
                            rounded
                        ></v-textarea>
                        <v-text-field
                            class="d-none"
                            name="_hidden"
                            v-model="form._hidden"
                            type="hidden"
                        ></v-text-field>
                        <v-btn
                            type="submit"
                            color="primary"
                            :loading="form.loading"
                            block
                            rounded
                            >Contact me</v-btn
                        >
                    </v-form>
                </v-theme-provider>
            </v-container>
            <v-snackbar :color="snackbar.color" v-model="snackbar.active">{{
                snackbar.message
            }}</v-snackbar>
        </v-parallax>
    </v-app>
</template>
