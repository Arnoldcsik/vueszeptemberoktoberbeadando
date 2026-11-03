
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const uzenet = ref('Az oldal betöltése folyamatban...')
const datum = ref('')
const szamlalo = ref(0)
const masodpercek = ref(0)

let idozito = null

// A komponens betöltődésekor lefut
onMounted(() => {
    uzenet.value = 'A Vue komponens sikeresen betöltődött!'
    datum.value = new Date().toLocaleString('hu-HU')

    idozito = setInterval(() => {
        masodpercek.value++
    }, 1000)
})

// A komponens eltávolításakor leállítjuk az időzítőt
onUnmounted(() => {
    clearInterval(idozito)
})

// Számláló növelése
function novel() {
    szamlalo.value++
}
</script>

<template>
    <main class="container">

        <header>
            <h1>Vue.js – onMounted</h1>
            <p>Életciklus-hook bemutatása</p>
        </header>

        <section class="card">
            <h2>Mi az az onMounted?</h2>

            <p>
                Az onMounted() a Vue.js egyik életciklus-hookja.
                Akkor fut le, amikor a komponens már bekerült
                a DOM-ba, vagyis megjelent a weboldalon.
            </p>

            <p>
                Segítségével olyan műveleteket hajthatunk végre,
                amelyeknek csak a komponens betöltődése után
                kell elindulniuk.
            </p>
        </section>

        <section class="card">
            <h2>Működő példa</h2>

            <div class="result">
                <p><strong>Állapot:</strong></p>
                <p>{{ uzenet }}</p>

                <p><strong>Betöltés időpontja:</strong></p>
                <p>{{ datum }}</p>

                <p><strong>Eltelt idő:</strong></p>
                <p>{{ masodpercek }} másodperc</p>
            </div>
        </section>

        <section class="card">
            <h2>Kattintásszámláló</h2>

            <p>
                Kattintások száma:
                <strong>{{ szamlalo }}</strong>
            </p>

            <button @click="novel">
                Számláló növelése
            </button>
        </section>

        <section class="card">
            <h2>onMounted példakód</h2>

            <pre><code>import { ref, onMounted } from 'vue'

const uzenet = ref('Betöltés...')

onMounted(() => {
    uzenet.value = 'A komponens betöltődött!'
})</code></pre>
        </section>

        <section class="card">
            <h2>A működés magyarázata</h2>

            <ol>
                <li>Az onMounted hookot importáljuk a Vue-ból.</li>
                <li>A ref segítségével létrehozunk egy reaktív változót.</li>
                <li>Az onMounted() függvényben megadjuk a végrehajtandó műveletet.</li>
                <li>Amikor a komponens bekerül a DOM-ba, a függvény automatikusan lefut.</li>
                <li>A változók értékei frissülnek, és a Vue megjeleníti az új adatokat.</li>
            </ol>
        </section>

        <section class="card">
            <h2>Mire használható az onMounted?</h2>

            <ul>
                <li>Adatok betöltésére.</li>
                <li>API-kérések indítására.</li>
                <li>Időzítők elindítására.</li>
                <li>Külső könyvtárak inicializálására.</li>
                <li>DOM-elemek kezelésének megkezdésére.</li>
            </ul>
        </section>

        <section class="card">
            <h2>Összefoglalás</h2>

            <p>
                Az onMounted() egy fontos Vue életciklus-hook,
                amely a komponens megjelenése után hajtja végre
                a megadott JavaScript-kódot.
            </p>

            <p>
                Segítségével könnyedén kezelhetjük a betöltéshez
                kapcsolódó feladatokat, például az adatok
                lekérését vagy az időzítők indítását.
            </p>
        </section>

        <footer>
            Vue.js 3 – onMounted bemutató
        </footer>

    </main>
</template>
