<script setup lang="ts">
import { onMounted, ref } from 'vue'

type FriendLink = {
  name: string
  url: string
}

const friendLinks = ref<FriendLink[]>([])
const pending = ref(true)
const failed = ref(false)

async function loadFriendLinks() {
  try {
    const response = await fetch('https://api.aoe.top/api/friendly/links')
    if (!response.ok) {
      throw new Error(`Failed to load links: ${response.status}`)
    }

    const data = await response.json()
    friendLinks.value = Array.isArray(data) ? data : []
  } catch (error) {
    console.error(error)
    failed.value = true
  } finally {
    pending.value = false
  }
}

onMounted(loadFriendLinks)
</script>
<template>
  <div class="min-h-screen bg-background text-foreground flex flex-col">
    <main class="flex-1">
      <router-view />
    </main>

    <footer class="border-t border-border/60 bg-background/80 backdrop-blur">
      <div class="mx-auto w-full max-w-6xl px-4 py-5 sm:px-6 lg:px-8">
        <div>
          <div>
            <p class="text-[12px] font-semibold tracking-[0.12em] text-muted-foreground uppercase">友情链接</p>
          </div>

          <div
            v-if="pending"
            class="mt-2 px-0 py-[0.2rem] text-[12px] text-muted-foreground/80"
          >
            友链加载中...
          </div>
          <div
            v-else-if="failed"
            class="mt-2 px-0 py-[0.2rem] text-[12px] text-muted-foreground/80"
          >
            友链加载失败，请稍后重试。
          </div>
          <div v-else class="mt-2 flex flex-wrap gap-x-2 gap-y-1">
            <a
              v-for="link in friendLinks"
              :key="link.url"
              :href="link.url"
              target="_blank"
              rel="noopener noreferrer"
              class="rounded-full px-[0.4rem] py-[0.2rem] text-[12px] leading-[1.4] text-foreground/70 transition hover:text-primary"
            >
              {{ link.name }}
            </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>
<style scoped></style>
