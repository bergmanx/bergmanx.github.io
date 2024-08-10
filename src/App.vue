<script setup>
const name = "Bergman";
const socials = [{ icon: "mdi-github", link: "https://github.com/bergmanx" }];
const stackImages = ["python.png", "vue.png", "javascript.png"];
const projects = [];
const parallax = "parallax.png";
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
                    <v-form>
                        <v-text-field
                            placeholder="Your name"
                            variant="solo"
                            rounded
                        ></v-text-field>
                        <v-text-field
                            type="email"
                            placeholder="Your email"
                            variant="solo"
                            rounded
                        ></v-text-field>
                        <v-textarea
                            placeholder="Message"
                            variant="solo"
                            rounded
                        ></v-textarea>
                        <v-btn color="primary" block rounded>Contact me</v-btn>
                    </v-form>
                </v-theme-provider>
            </v-container>
        </v-parallax>
    </v-app>
</template>
