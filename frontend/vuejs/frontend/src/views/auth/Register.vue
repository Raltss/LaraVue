<script setup lang="ts">
import axios from "axios";

axios.defaults.withCredentials = true;
axios.defaults.withXSRFToken = true;
axios.defaults.baseURL = "http://localhost:8000";

const register = async () => {
    console.log("Registering..");
    await axios.get("/sanctum/csrf-cookie");
    try {
        const response = await axios.post("/api/register", {
            name : "John Doe",
            email : "john@doe.com",
            password : "password",
            password_confirmation : "password",
        });
        console.log(response.data);
     } catch (error) {
        console.log("Full error:", error);
        console.log("Response data:", error.response?.data);
        console.log("Validation errors:", error.response?.data?.errors);
     }
};

</script>

<template>
    <button @click="register">Register Now</button>
</template>
