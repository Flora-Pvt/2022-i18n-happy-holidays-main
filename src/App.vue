<template>
  <main class="flex flex-col justify-center h-full mx-auto max-w-600px">
    <section class="flex flex-col items-center leading-loose text-center">
      <div class="text-3xl mb-20">
        <span class="i-twemoji-christmas-tree"></span>
        {{ $t('happyHolidays') }}
        <span class="i-twemoji-world-map"></span>
      </div>

      <fieldset>
        <div
          v-for="locale in $i18n.availableLocales"
          :key="`locale-${locale}`"
          class="w-full flex"
        >
          <input
            v-model="$i18n.locale"
            :value="locale"
            type="radio"
            id="language"
            name="language"
            checked
          />
          <label for="language">
            <span class="mx-2" :class="flags[locale]"></span>
            <span v-t="{ path: 'language', locale }"></span>
          </label>
        </div>
      </fieldset>

      <!-- Flags - the current locale -->
    </section>
  </main>
</template>

<script setup>
import { useI18n } from 'vue-i18n'

const flags = {
  en: 'i-twemoji-flag-united-states',
  de: 'i-twemoji-flag-germany',
  'ja-JP': 'i-twemoji-flag-japan',
}
// See the README about tricky timezone issues!
// I figured since this is i18n-friendly, we'd wanna
// make sure the timezones were right :-)
const christmasDate = new Date('2022/12/25')
</script>
