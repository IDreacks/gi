<script>
import { mapWritableState } from 'pinia';


import { useUserStore } from "../stores/counter";
import TheResult from "../components/TheResult.vue";

export default {
    data() {
        return {
            user: {
                poids: 0,
                taille: 0,
            },
        };
    },
    computed: {
        ...mapWritableState(useUserStore, ["poids", "taille", "imc"])
    },
    methods: {

        onCalcul() {
            if (this.user.poids <= 0 || this.user.taille <= 0) {
                this.user.taille = 0;
                this.user.poids = 0;
                console.log("error");
                return;
            }
            if (this.user.poids === "" || this.user.taille === "") {
                this.user.taille = 0;
                this.user.poids = 0;
                return;
            }
            (this.poids = this.store.poids),
                (this.taille = this.store.taille),
                (this.imc = this.poids / (this.taille * this.taille));
        },
    },
    components:
    {
        TheResult,
    }
}


</script>

<template>
    <form @submit.prevent="onCalcul">
        <input
            type="number"
            v-model="user.taille"
            name="taille"
            id="taille"
            placeholder="Votre taille en cm"
            required
            min="0"
        />
        <input
            type="number"
            v-model="user.poids"
            name="poids"
            id="poids"
            placeholder="Votre poids en kg"
            required
            min="0"
        />
        <input type="submit" name="submit" />
    </form>
     <TheResult />
</template>


<style scoped>
form {
    display: flex;
    flex-direction: column;
}
form input,
textarea,
h1 {
    width: 50%;
    margin: auto;
    padding: 10px;
    border-radius: 5px;
    outline: none;
    border-color: hsla(160, 100%, 37%, 1);
    color: white;
    background-color: #181818;
    margin-top: 2%;
}
label {
    margin: auto;
    color: hsla(160, 100%, 37%, 1);
}

#co-button {
    margin-top: 2%;
    width: 40%;
    color: hsla(160, 100%, 37%, 1);
    padding: 10px;
    cursor: pointer;
    background-color: #000000;
}
#co-button:hover {
    background-color: #181818;
}
</style>