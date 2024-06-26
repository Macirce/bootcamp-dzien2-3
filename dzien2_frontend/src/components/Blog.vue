<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <button @click="pobierzWpisy">refresh</button>
        siema blog!
        <div class="grid mx6 gap-4">
        <div v-for="wpis in wpisy" class="grid drop-shadow-x1 bg-stone-300">
            <p>{{ wpis }}</p>
        </div>
        </div>
        <input v-model="nowyBlog" type="text">
        <button @click="dodajWpisy" class="bg-blue-600 rounded=sm p-4 text-gray " >dodaj</button>
    </div>
</template>

<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';

export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async dodajWpisy() {
            await dzien2_backend.dodaj_wpis(this.nowyBlog);
        },
        async pobierzWpisy() {
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        }
    },
    async mounted(){
        this.pobierzWpisy()
    }
}
</script>