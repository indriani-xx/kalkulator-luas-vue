<script setup lang="ts">
import {ref} from 'vue'

const luasPP = ref<number | null>(null)
const hitungLuas = () => {
let p = Number(prompt('panjang : '))
let l = Number(prompt('lebar : '))

luasPP.value = p * l
}

const luasPersegi = ref<number | null>(null)
const hitungLuasPersegi = () => {
let s = Number(prompt('sisi : '))

luasPersegi.value = s*s
}

const luasSegiTiga = ref<number | null>(null)
const hitungLuasSegiTiga = () => {
let a = Number(prompt('alas : '))
let t = Number(prompt('tinggi : '))

luasSegiTiga.value = a * t /2
}

const luasLingkaran = ref<string | null>(null)
const hitungLuasLingkaran = () => {
const phi = 22/7
let r = Number(prompt('jari - jari : '))


luasLingkaran.value = (phi * r * r).toFixed(2)
}

const luasJaGen = ref<number | null>(null)
const hitungLuasJaGen = () => {
let a = Number(prompt('alas : '))
let t = Number(prompt('tinggi : '))

luasJaGen.value = a * t 
}

const luasTrapesium = ref<string | null>(null)
const hitungLuasTrapesium = () => {
let a = Number(prompt('sisi sejajar 1 : '))
let b = Number(prompt(' sisi sejajar 2 : '))
let t = Number(prompt('tinggi : '))

luasTrapesium.value = (0.5 * (a+b) * t).toFixed(2)
}

const luasKetupat = ref<string | null>(null)
const hitungLuasKetupat = () => {
let d1 = Number(prompt('diagonal 1 : '))
let d2 = Number(prompt('diagonal 2 : '))

luasKetupat.value = (d1 * d2 /2).toFixed(2)
}
</script>

<template>
  <div class="container">

    <div class="grid">
      <div class="card">
        <button class="btn" @click="hitungLuas">Luas Persegi Panjang</button>
        <p class="result">Hasil: <span>{{ luasPP ?? '-' }}</span></p>
      </div>

      <div class="card">
        <button class="btn" @click="hitungLuasPersegi">Luas Persegi</button>
        <p class="result">Hasil: <span>{{ luasPersegi ?? '-' }}</span></p>
      </div>

      <div class="card">
        <button class="btn" @click="hitungLuasSegiTiga">Luas Segitiga</button>
        <p class="result">Hasil: <span>{{ luasSegiTiga ?? '-' }}</span></p>
      </div>

      <div class="card">
        <button class="btn" @click="hitungLuasLingkaran">Luas Lingkaran</button>
        <p class="result">Hasil: <span>{{ luasLingkaran ?? '-' }}</span></p>
      </div>

      <div class="card">
        <button class="btn" @click="hitungLuasJaGen">Luas Jajar Genjang</button>
        <p class="result">Hasil: <span>{{ luasJaGen ?? '-' }}</span></p>
      </div>

      <div class="card">
        <button class="btn" @click="hitungLuasTrapesium">Luas Trapesium</button>
        <p class="result">Hasil: <span>{{ luasTrapesium ?? '-' }}</span></p>
      </div>

      <div class="card">
        <button class="btn" @click="hitungLuasKetupat">
          Luas Ketupat / Layang-layang
        </button>
        <p class="result">Hasil: <span>{{ luasKetupat ?? '-' }}</span></p>
      </div>
    </div>
  </div>
</template>


<style scoped>
.container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 40px 20px;
  font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
  min-height: 100vh;
}


.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 20px;
}

.card {
  background: #e5e4e4;
  border-radius: 16px;
  padding: 20px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 24px rgba(79, 70, 229, 0.15);
}

.btn {
  width: 100%;
  padding: 14px 18px;
  border: none;
  border-radius: 10px;
  font-size: 15px;
  font-weight: 600;
  color: #ffffff;
  cursor: pointer;
  background: linear-gradient(135deg, #4c4ebc 0%, #8b5cf6 100%);
  box-shadow: 0 4px 10px rgba(99, 102, 241, 0.35);
  transition: all 0.25s ease;
  letter-spacing: 0.3px;
}

.btn:hover {
  background: linear-gradient(135deg, #4b43d7 0%, #6f36d0 100%);
  box-shadow: 0 6px 16px rgba(99, 102, 241, 0.5);
  transform: translateY(-2px);
}

.btn:active {
  transform: translateY(0);
  box-shadow: 0 2px 6px rgba(99, 102, 241, 0.4);
}

.btn:focus-visible {
  outline: 3px solid rgba(139, 92, 246, 0.4);
  outline-offset: 2px;
}

.result {
  text-align: center;
  font-size: 14px;
  color: #64748b;
  margin: 0;
}

.result span {
  display: inline-block;
  margin-left: 4px;
  font-weight: 700;
  color: #4f46e5;
  font-size: 16px;
}
</style>