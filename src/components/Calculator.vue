<script setup lang="ts">
import { computed, ref } from 'vue'

// Tipos das operações
type Operacao = 'somar' | 'subtrair' | 'multiplicar' | 'dividir'

// Valores dos inputs (como string)
const numero1 = ref<string>('')
const numero2 = ref<string>('')
const operacao = ref<Operacao>('somar')

// Converte string para número
const valor1 = computed<number>(() => Number(numero1.value.replace(',', '.')))
const valor2 = computed<number>(() => Number(numero2.value.replace(',', '.')))

// Calcula automaticamente o resultado
const resultado = computed<string>(() => {
  // Se algum campo estiver vazio
  if (numero1.value === '' || numero2.value === '') {
    return '—'
  }

  // Se não for um número válido
  if (isNaN(valor1.value) || isNaN(valor2.value)) {
    return 'Número inválido'
  }

  // Faz o cálculo baseado na operação
  switch (operacao.value) {
    case 'somar':
      return (valor1.value + valor2.value).toString()
    case 'subtrair':
      return (valor1.value - valor2.value).toString()
    case 'multiplicar':
      return (valor1.value * valor2.value).toString()
    case 'dividir':
      if (valor2.value === 0) {
        return 'Não pode dividir por zero'
      }
      return (valor1.value / valor2.value).toString()
    default:
      return '—'
  }
})
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 flex items-center justify-center p-4">
    <div class="max-w-md w-full bg-white rounded-2xl shadow-xl p-8 backdrop-blur-sm">
      <!-- Cabeçalho -->
      <div class="text-center mb-8">
        <div class="w-16 h-16 bg-gradient-to-r from-blue-500 to-indigo-600 rounded-full mx-auto mb-4 flex items-center justify-center">
          <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"></path>
          </svg>
        </div>
        <h1 class="text-3xl font-bold text-gray-800 mb-2">
          Calculadora
        </h1>
        <p class="text-gray-600">Faça seus cálculos de forma simples</p>
      </div>

      <!-- Primeiro número -->
      <div class="mb-6">
        <label class="block text-sm font-semibold text-gray-700 mb-3">
          📊 Primeiro número:
        </label>
        <input
          v-model="numero1"
          type="text"
          inputmode="decimal"
          placeholder="Digite um número"
          class="w-full px-4 py-3 text-lg border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:ring-4 focus:ring-blue-100 transition-all duration-200 bg-gray-50 focus:bg-white"
        />
      </div>

      <!-- Operação -->
      <div class="mb-6">
        <label class="block text-sm font-semibold text-gray-700 mb-3">
          ⚡ Operação:
        </label>
        <select
          v-model="operacao"
          class="w-full px-4 py-3 text-lg border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:ring-4 focus:ring-blue-100 transition-all duration-200 bg-gray-50 focus:bg-white cursor-pointer"
        >
          <option value="somar">➕ Somar (+)</option>
          <option value="subtrair">➖ Subtrair (-)</option>
          <option value="multiplicar">✖️ Multiplicar (×)</option>
          <option value="dividir">➗ Dividir (÷)</option>
        </select>
      </div>

      <!-- Segundo número -->
      <div class="mb-8">
        <label class="block text-sm font-semibold text-gray-700 mb-3">
          📊 Segundo número:
        </label>
        <input
          v-model="numero2"
          type="text"
          inputmode="decimal"
          placeholder="Digite um número"
          class="w-full px-4 py-3 text-lg border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:ring-4 focus:ring-blue-100 transition-all duration-200 bg-gray-50 focus:bg-white"
        />
      </div>

      <!-- Resultado -->
      <div class="relative">
        <div class="bg-gradient-to-r from-green-50 to-emerald-50 border-2 border-green-200 rounded-2xl p-6 shadow-inner">
          <div class="flex items-center justify-between mb-2">
            <span class="text-sm font-semibold text-green-700 flex items-center">
              🎯 Resultado:
            </span>
            <div class="w-3 h-3 bg-green-400 rounded-full animate-pulse"></div>
          </div>
          <div class="text-3xl font-bold text-green-800 break-all">
            {{ resultado }}
          </div>
        </div>
        
        <!-- Indicador de cálculo automático -->
        <div class="mt-4 text-center">
          <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-blue-100 text-blue-800">
            ⚡ Cálculo automático ativo
          </span>
        </div>
      </div>

      <!-- Rodapé -->
      <div class="mt-8 text-center">
        <p class="text-xs text-gray-500">
          Digite os números e veja o resultado na hora! 🚀
        </p>
      </div>
    </div>
  </div>
</template>
