<script setup lang="ts">
import { reactive } from 'vue'

type Shape = {
  id: string
  label: string
  inputs: string[]
  calculate: (values: number[]) => number
}

const shapes: Shape[] = [
  {
    id: 'rectangle',
    label: 'Persegi Panjang',
    inputs: ['Panjang', 'Lebar'],
    calculate: ([length = 0, width = 0]) => length * width,
  },
  {
    id: 'square',
    label: 'Persegi',
    inputs: ['Sisi'],
    calculate: ([side = 0]) => side * side,
  },
  {
    id: 'triangle',
    label: 'Segitiga',
    inputs: ['Alas', 'Tinggi'],
    calculate: ([base = 0, height = 0]) => (base * height) / 2,
  },
  {
    id: 'circle',
    label: 'Lingkaran',
    inputs: ['Jari-jari'],
    calculate: ([radius = 0]) => Math.PI * radius * radius,
  },
  {
    id: 'parallelogram',
    label: 'Jajar Genjang',
    inputs: ['Alas', 'Tinggi'],
    calculate: ([base = 0, height = 0]) => base * height,
  },
  {
    id: 'trapezoid',
    label: 'Trapesium',
    inputs: ['Sisi sejajar 1', 'Sisi sejajar 2', 'Tinggi'],
    calculate: ([firstSide = 0, secondSide = 0, height = 0]) =>
      ((firstSide + secondSide) * height) / 2,
  },
  {
    id: 'kite',
    label: 'Belah Ketupat / Layang-layang',
    inputs: ['Diagonal 1', 'Diagonal 2'],
    calculate: ([firstDiagonal = 0, secondDiagonal = 0]) =>
      (firstDiagonal * secondDiagonal) / 2,
  },
]

const results = reactive<Record<string, number>>({})

function promptForPositiveNumber(label: string): number | null {
  const input = prompt(`${label}:`)

  if (input === null) {
    return null
  }

  const value = Number(input)
  if (!Number.isFinite(value) || value <= 0) {
    alert('Masukkan angka yang valid dan lebih besar dari 0.')
    return null
  }

  return value
}

function calculateArea(shape: Shape) {
  const values: number[] = []

  for (const inputLabel of shape.inputs) {
    const value = promptForPositiveNumber(inputLabel)
    if (value === null) {
      return
    }

    values.push(value)
  }

  results[shape.id] = shape.calculate(values)
}

function formatResult(value: number | undefined): string {
  return value === undefined ? '-' : value.toFixed(2)
}
</script>

<template>
  <div class="container">
    <div class="grid">
      <div v-for="shape in shapes" :key="shape.id" class="card">
        <button class="btn" type="button" @click="calculateArea(shape)">
          Luas {{ shape.label }}
        </button>
        <p class="result">
          Hasil: <span>{{ formatResult(results[shape.id]) }}</span>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 1000px;
  min-height: 100vh;
  margin: 0 auto;
  padding: 40px 20px;
  font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 20px;
}

.card {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding: 20px;
  background: #e5e4e4;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgb(0 0 0 / 6%);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 24px rgb(79 70 229 / 15%);
}

.btn {
  width: 100%;
  padding: 14px 18px;
  color: #fff;
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 0.3px;
  cursor: pointer;
  background: linear-gradient(135deg, #4c4ebc 0%, #8b5cf6 100%);
  border: 0;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgb(99 102 241 / 35%);
  transition: transform 0.25s ease, box-shadow 0.25s ease, background 0.25s ease;
}

.btn:hover {
  background: linear-gradient(135deg, #4b43d7 0%, #6f36d0 100%);
  box-shadow: 0 6px 16px rgb(99 102 241 / 50%);
  transform: translateY(-2px);
}

.btn:active {
  box-shadow: 0 2px 6px rgb(99 102 241 / 40%);
  transform: translateY(0);
}

.btn:focus-visible {
  outline: 3px solid rgb(139 92 246 / 40%);
  outline-offset: 2px;
}

.result {
  margin: 0;
  color: #64748b;
  font-size: 14px;
  text-align: center;
}

.result span {
  display: inline-block;
  margin-left: 4px;
  color: #4f46e5;
  font-size: 16px;
  font-weight: 700;
}
</style>
