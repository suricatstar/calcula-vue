<script setup lang="ts">
import { computed, ref } from 'vue'

type Operacao = 'somar' | 'subtrair' | 'multiplicar' | 'dividir'

const numero1 = ref<number | null>(null)
const numero2 = ref<number | null>(null)
const operacao = ref<Operacao>('somar')

const valor1 = computed<number>(() => {
  if (numero1.value === null || numero1.value === undefined) return 0
  const str = String(numero1.value)
  return Number(str.replace(',', '.'))
})

const valor2 = computed<number>(() => {
  if (numero2.value === null || numero2.value === undefined) return 0
  const str = String(numero2.value)
  return Number(str.replace(',', '.'))
})

const resultado = computed<string>(() => {
  if (numero1.value === null || numero2.value === null || numero1.value === undefined || numero2.value === undefined) {
    return '0'
  }

  if (isNaN(valor1.value) || isNaN(valor2.value)) {
    return 'Erro'
  }

  switch (operacao.value) {
    case 'somar':
      return (valor1.value + valor2.value).toString()
    case 'subtrair':
      return (valor1.value - valor2.value).toString()
    case 'multiplicar':
      return (valor1.value * valor2.value).toString()
    case 'dividir':
      if (valor2.value === 0) {
        return 'Erro'
      }
      return (valor1.value / valor2.value).toString()
    default:
      return '0'
  }
})
</script>

<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-4">
    <div class="bg-white rounded-lg shadow-lg p-6 w-full max-w-sm">
      
      <!-- Título -->
      <h1 class="text-2xl font-bold text-center mb-6 text-gray-800">
        Calculadora
      </h1>

      <!-- Resultado (Display) -->
      <div class="bg-gray-900 text-white p-4 rounded-lg mb-6 text-right">
        <div class="text-3xl font-mono">{{ resultado }}</div>
      </div>

      <!-- Primeiro número -->
      <div class="mb-4">
        <label class="block text-sm font-medium text-gray-700 mb-2">
          Primeiro número
        </label>
        <input
          v-model.number="numero1"
          type="number"
          placeholder="0"
          class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
        />
      </div>

      <!-- Operação -->
      <div class="mb-4">
        <label class="block text-sm font-medium text-gray-700 mb-2">
          Operação
        </label>
        <select
          v-model="operacao"
          class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
        >
          <option value="somar">+ Somar</option>
          <option value="subtrair">- Subtrair</option>
          <option value="multiplicar">× Multiplicar</option>
          <option value="dividir">÷ Dividir</option>
        </select>
      </div>

      <!-- Segundo número -->
      <div class="mb-6">
        <label class="block text-sm font-medium text-gray-700 mb-2">
          Segundo número
        </label>
        <input
          v-model.number="numero2"
          type="number"
          placeholder="0"
          class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
        />
      </div>

      <!-- Info -->
      <p class="text-xs text-gray-500 text-center">
        O resultado é calculado automaticamente
      </p>

    </div>
  </div>
</template>
