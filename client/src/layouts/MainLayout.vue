<template>
  <q-layout view="lHh Lpr lFf">
    <transition name="fade">
      <LoadingScreen v-if="isLoading" />
    </transition>
    <q-header elevated>
      <q-toolbar>


        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>



    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import { supabase } from 'src/ultis/supabase.js'
import LoadingScreen from 'components/LoadingScreen.vue'

const router = useRouter()
const isLoading = ref(true)

onMounted(() => {
  if (!document.getElementById('turnstile-script')) {
    const script = document.createElement('script')
    script.id = 'turnstile-script'
    script.src = 'https://challenges.cloudflare.com/turnstile/v0/api.js?render=explicit'
    script.async = true
    script.defer = true
    document.head.appendChild(script)
  }

  const renderTurnstile = () => {
    if (window.turnstile) {
      window.turnstile.render('#my-turnstile', {
        sitekey: '0x4AAAAAAC9DYzg2iBTLuDzs',
        callback: async (token) => {
          try {
            const { data, error } = await supabase.auth.signInAnonymously({
              options: {
                captchaToken: token,
              },
            })
          
            if (error) throw error

            isLoading.value = false
            router.push('/party')
          } catch (err) {
            console.error('Anonymous sign-in error:', err.message)
            // You can handle error notifications here
          }
        },
      })
    } else {
      setTimeout(renderTurnstile, 250)
    }
  }
  
  renderTurnstile()
})

const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.6s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
