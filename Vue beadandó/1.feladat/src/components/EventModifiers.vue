<script setup>
import { ref } from 'vue'

const uzenet = ref('')
const kattintasok = ref(0)
const egyszeriKattintasok = ref(0)

function kuldes() {
    uzenet.value = 'Az űrlap sikeresen elküldve!'
}

function szuloKattintas() {
    uzenet.value = 'A szülőelemre kattintottál!'
}

function gombKattintas() {
    uzenet.value = 'A belső gombra kattintottál!'
}

function novel() {
    kattintasok.value++
}
</script>

<template>
    <main class="container">

        <header>
            <h1>Vue.js – Event Modifiers</h1>
            <p>Eseménymódosítók bemutatása</p>
        </header>

        <section class="card">
            <h2>Mi az a Vue Event Modifiers?</h2>

            <p>
                A Vue Event Modifiers olyan eseménymódosítók,
                amelyekkel szabályozhatjuk a felhasználói
                események működését.
            </p>

            <p>
                A Vue eseménykezelésére a v-on direktíva
                használható, amelynek rövidített formája
                a @ karakter.
            </p>
        </section>

        <section class="card">
            <h2>1. Prevent módosító</h2>

            <p>
                Megakadályozza az alapértelmezett
                böngészőműveletet.
            </p>

            <form @submit.prevent="kuldes">
                <button type="submit">
                    Űrlap elküldése
                </button>
            </form>

            <pre><code>&lt;form @submit.prevent="kuldes"&gt;</code></pre>
        </section>

        <section class="card">
            <h2>2. Once módosító</h2>

            <p>
                Az eseménykezelő csak egyszer hajtódik végre.
            </p>

            <button @click.once="egyszeriKattintasok++">
                Kattints ide!
            </button>

            <p>
                Sikeres kattintások:
                {{ egyszeriKattintasok }}
            </p>

            <pre><code>&lt;button @click.once="egyszeriKattintasok++"&gt;</code></pre>
        </section>

        <section class="card">
            <h2>3. Stop módosító</h2>

            <p>
                Megakadályozza az esemény továbbterjedését
                a szülőelem felé.
            </p>

            <div class="result" @click="szuloKattintas">
                Szülőelem

                <button @click.stop="gombKattintas">
                    Belső gomb
                </button>
            </div>

            <pre><code>&lt;button @click.stop="gombKattintas"&gt;</code></pre>
        </section>

        <section class="card">
            <h2>4. Self módosító</h2>

            <p>
                Csak akkor fut le az eseménykezelő,
                ha közvetlenül az adott elemre kattintunk.
            </p>

            <div
                class="result"
                @click.self="uzenet = 'A dobozra kattintottál!'"
            >
                Kattints a doboz üres területére!

                <button @click="gombKattintas">
                    Belső gomb
                </button>
            </div>

            <pre><code>&lt;div @click.self="kattintas"&gt;</code></pre>
        </section>

        <section class="card">
            <h2>5. Capture módosító</h2>

            <p>
                Az eseménykezelés a capture fázisban történik,
                tehát a szülő eseménykezelője a gyermeké előtt fut le.
            </p>

            <div class="result" @click.capture="szuloKattintas">
                Szülőelem

                <button @click="gombKattintas">
                    Kattints ide!
                </button>
            </div>

            <pre><code>&lt;div @click.capture="szuloKattintas"&gt;</code></pre>
        </section>

        <section class="card">
            <h2>6. Passive módosító</h2>

            <p>
                Jelzi a böngészőnek, hogy az eseménykezelő
                nem fogja megakadályozni az alapértelmezett
                böngészőműveletet.
            </p>

            <div class="result scroll-box" @scroll.passive="novel">
                <p v-for="i in 20" :key="i">
                    Görgethető tartalom {{ i }}
                </p>
            </div>

            <p>Görgetési események: {{ kattintasok }}</p>

            <pre><code>&lt;div @scroll.passive="novel"&gt;</code></pre>
        </section>

        <section class="card">
            <h2>Visszajelzés</h2>

            <p class="message">
                {{ uzenet || 'Még nem történt esemény.' }}
            </p>
        </section>

        <section class="card">
            <h2>Összefoglalás</h2>

            <p>
                A Vue Event Modifiers segítségével egyszerűen
                szabályozhatjuk az események működését.
                Segítségükkel csökkenthető a szükséges
                JavaScript-kód mennyisége, és átláthatóbbá
                válik az eseménykezelés.
            </p>
        </section>

        <footer>
            Vue.js 3 – Event Modifiers
        </footer>

    </main>
</template>