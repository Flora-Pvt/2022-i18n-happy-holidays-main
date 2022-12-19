<template>
  <main class="flex flex-col justify-center h-full mx-auto max-w-600px">
    <section class="flex flex-col items-center leading-loose text-center">
      <p class="text-3xl mb-6">
        <i class="i-twemoji-christmas-tree" />
        {{ $t('happyHolidays') }}
        <i class="i-twemoji-world-map" />
      </p>

      <i18n-t keypath="christmasIsComing" tag="p" class="text-xl mb-16">
        <template #date>
          {{ $d(christmasDate, 'long') }}
        </template>

        <template #time>
          <span class="font-medium text-green-600">
            {{ $t('day', daysRemaining) }}
          </span>
        </template>
      </i18n-t>

      <fieldset>
        <div
          v-for="locale in $i18n.availableLocales"
          :key="`locale-${locale}`"
          class="w-full flex"
        >
          <input
            v-model="$i18n.locale"
            :value="locale"
            :id="locale"
            name="language"
            type="radio"
            checked
          />
          <label :for="locale">
            <i class="mx-2" :class="flags[locale]" />
            <span v-t="{ path: 'language', locale }"></span>
          </label>
        </div>
      </fieldset>
    </section>
  </main>
</template>

<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const christmasDate = new Date('2022/12/25')
const timeRemaining = christmasDate.getTime() - Date.now()
const oneDay = 24 * 60 * 60 * 1000
const daysRemaining = Math.ceil(timeRemaining / oneDay)

const flags = {
  en: 'i-twemoji-flag-united-states',
  de: 'i-twemoji-flag-germany',
  'ja-JP': 'i-twemoji-flag-japan',
}
</script>
