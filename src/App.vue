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
      <div class="mx-auto w-full max-w-6xl px-4 py-10 sm:px-6 lg:px-8">
        <div class="rounded-[2rem] border border-border/60 bg-card/70 p-6 shadow-sm">
          <div>
            <p class="text-sm font-semibold tracking-[0.24em] text-primary uppercase">友情链接</p>
            <p class="mt-2 text-sm text-muted-foreground">实时同步站群最新友链，为 Glosc AI 首页补齐统一底部入口。</p>
          </div>

          <div v-if="pending" class="mt-5 rounded-2xl border border-border/50 bg-background/70 px-4 py-3 text-sm text-muted-foreground">
            友链加载中...
          </div>
          <div v-else-if="failed" class="mt-5 rounded-2xl border border-border/50 bg-background/70 px-4 py-3 text-sm text-muted-foreground">
            友链加载失败，请稍后重试。
          </div>
          <div v-else class="mt-5 flex flex-wrap gap-3">
            <a
              v-for="link in friendLinks"
              :key="link.url"
              :href="link.url"
              target="_blank"
              rel="noopener noreferrer"
              class="rounded-full border border-border/70 bg-background px-4 py-2 text-sm text-foreground/80 transition hover:-translate-y-0.5 hover:border-primary/50 hover:text-primary"
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
