<template>
    <table>
        <thead>
            <tr>
                <th>Taille</th>
                <th>Poids</th>
                <th>Imc</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>{{ getPoids * 100}}</td>
                <td>{{ getTaille }}</td>
                <td>{{ getImc }}</td>
            </tr>
        </tbody>
    </table>
</template>

<script lang="ts">
import { useUserStore } from "@/stores/counter";
import { mapState } from "pinia";
export default {
    computed: {
        ...mapState(useUserStore, ["getTaille", "getPoids", "getImc"])
    }
}
</script>