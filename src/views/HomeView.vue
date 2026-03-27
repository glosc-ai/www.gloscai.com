<script setup lang="ts">
import { markRaw } from 'vue'
import { ArrowRight, ArrowUpRight, Github, LockKeyhole, Workflow } from 'lucide-vue-next'

import { Button } from '@/components/ui/button'

const products = [
  {
    name: 'Copilot',
    description: 'AI 助手与协作入口。',
    href: 'https://copilot.gloscai.com/',
  },
  {
    name: 'Nutri',
    description: '营养与健康产品。',
    href: 'https://nutri.gloscai.com/',
  },
  {
    name: 'Cat',
    description: '对话式工具实验。',
    href: 'https://cat.gloscai.com/',
  },
  {
    name: '2FA',
    description: '认证与安全能力。',
    href: 'https://2fa.gloscai.com/',
  },
]

const capabilities = ['AI 产品落地', '工程化协作', '安全优先']
</script>

<template>
  <div class="relative overflow-hidden">
    <div class="pointer-events-none absolute inset-0">
      <div class="absolute left-[-10%] top-20 h-72 w-72 rounded-full bg-cyan-400/12 blur-3xl" />
      <div class="absolute right-[-8%] top-32 h-96 w-96 rounded-full bg-sky-500/10 blur-3xl" />
    </div>

    <section class="relative">
      <div class="mx-auto flex max-w-7xl flex-col px-6 pb-14 pt-6 lg:px-10">
        <header
          class="flex flex-wrap items-center justify-between gap-4 rounded-full border border-white/10 bg-white/5 px-5 py-3 backdrop-blur-xl"
        >
          <a
            href="#top"
            class="flex items-center gap-3 text-sm font-medium tracking-[0.24em] text-white/88 uppercase"
          >
            <img src="/favicon.ico" alt="Glosc AI" class="h-5 w-5" />
            Glosc AI
          </a>

          <nav class="flex flex-wrap items-center gap-5 text-sm text-white/65">
            <a href="#products" class="hover:text-white">产品</a>
            <a href="#open-source" class="hover:text-white">开源</a>
          </nav>
        </header>

        <div id="top" class="grid flex-1 gap-12 py-16">
          <div>
            <h1
              class="mt-7 text-5xl font-semibold leading-tight text-white sm:text-6xl lg:text-7xl"
            >
              Glosc
              <span class="text-cyan-300">AI</span>
            </h1>

            <p class="mt-6 text-lg leading-8 text-slate-300">
              一家刚起步的 AI 组织, 专注于构建实用的 AI
              产品与工具，持续沉淀开源能力，并以安全为核心原则。
              开发一些有用的东西，感谢每一位支持我们的朋友！
            </p>

            <div class="mt-9 flex flex-col gap-4 sm:flex-row">
              <Button
                as="a"
                href="#products"
                size="lg"
                class="rounded-full px-7 shadow-lg shadow-primary/20"
              >
                查看产品
                <ArrowRight class="size-4" />
              </Button>
              <Button
                as="a"
                href="https://github.com/glosc-ai"
                target="_blank"
                rel="noreferrer"
                variant="outline"
                size="lg"
                class="rounded-full border-white/15 bg-white/6 px-7 text-white hover:bg-white/10"
              >
                GitHub 组织
                <ArrowUpRight class="size-4" />
              </Button>
            </div>

            <div class="mt-10 grid gap-3 sm:grid-cols-3">
              <div
                v-for="item in capabilities"
                :key="item"
                class="rounded-2xl bg-white/4 px-4 py-4 text-sm text-slate-300 backdrop-blur"
              >
                {{ item }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="products" class="relative border-t border-white/10">
      <div class="mx-auto max-w-7xl px-6 py-24 lg:px-10">
        <div class="flex flex-col gap-4 md:flex-row md:items-end md:justify-between">
          <div>
            <p class="text-sm uppercase tracking-[0.24em] text-cyan-200/70">Products</p>
            <h2 class="mt-3 text-3xl font-semibold text-white sm:text-4xl">产品矩阵</h2>
          </div>
        </div>

        <div class="mt-10 grid gap-5 md:grid-cols-2 xl:grid-cols-4">
          <a
            v-for="product in products"
            :key="product.name"
            :href="product.href"
            target="_blank"
            rel="noreferrer"
            class="group rounded-3xl border border-white/10 bg-white/5 p-6 backdrop-blur transition duration-300 hover:-translate-y-1 hover:border-cyan-300/30 hover:bg-white/7"
          >
            <div class="flex items-center justify-between gap-4">
              <div class="flex items-center justify-center gap-4">
                <img
                  class="rounded-xl h-12 w-12"
                  :src="product.href + 'favicon.ico'"
                  :alt="product.name"
                />
                <h3 class="text-2xl font-medium text-white">{{ product.name }}</h3>
              </div>
              <ArrowUpRight class="size-5 text-slate-500 transition group-hover:text-cyan-300" />
            </div>
            <div class="mt-8 inline-flex items-center gap-2 text-sm text-cyan-200">
              访问产品
              <ArrowRight class="size-4" />
            </div>
          </a>
        </div>
      </div>
    </section>

    <section id="open-source" class="relative border-t border-white/10">
      <div class="mx-auto max-w-7xl px-6 py-24 lg:px-10">
        <div class="grid gap-8 lg:grid-cols-[minmax(0,1.1fr)_minmax(0,0.9fr)] lg:items-stretch">
          <div
            class="rounded-4xl border border-white/10 bg-linear-to-br from-white/7 to-white/2 p-8 backdrop-blur-xl"
          >
            <p class="text-sm uppercase tracking-[0.24em] text-cyan-200/70">Open Source</p>
            <h2 class="mt-4 text-3xl font-semibold text-white sm:text-4xl">开源组织与工程沉淀</h2>
            <p class="mt-5 max-w-xl text-base leading-8 text-slate-300">
              在 GitHub 持续沉淀组件、工具链与实验项目。
            </p>

            <div class="mt-8 flex flex-col gap-4 sm:flex-row">
              <Button
                as="a"
                href="https://github.com/glosc-ai"
                target="_blank"
                rel="noreferrer"
                size="lg"
                class="rounded-full px-7"
              >
                访问 Glosc AI
                <Github class="size-4" />
              </Button>
            </div>
          </div>

          <div class="grid gap-4">
            <div class="rounded-[1.75rem] border border-white/10 bg-slate-950/45 p-6">
              <p class="text-sm uppercase tracking-[0.18em] text-slate-500">Workflow</p>
              <p class="mt-3 text-xl font-medium text-white">产品与工程协同推进。</p>
            </div>
            <div class="rounded-[1.75rem] border border-white/10 bg-slate-950/45 p-6">
              <p class="text-sm uppercase tracking-[0.18em] text-slate-500">Shipping</p>
              <p class="mt-3 text-xl font-medium text-white">更快验证，更快上线。</p>
            </div>
            <div class="rounded-[1.75rem] border border-white/10 bg-slate-950/45 p-6">
              <p class="text-sm uppercase tracking-[0.18em] text-slate-500">Security</p>
              <p class="mt-3 text-xl font-medium text-white">认证与安全是基础设施。</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <footer id="footer" class="border-t border-white/10">
      <div
        class="mx-auto flex max-w-7xl flex-col gap-8 px-6 py-10 text-sm text-slate-400 lg:flex-row lg:items-end lg:justify-between lg:px-10"
      >
        <div>
          <p class="text-base font-medium text-white">Glosc AI</p>
          <p class="mt-4">© 2026 Glosc AI. 保留所有权利。</p>
          <p class="mt-2">
            <a href="https://beian.miit.gov.cn/" target="_blank" rel="noopener noreferrer"
              >沪ICP备2026003781号-1</a
            >
          </p>
          <p class="mt-2">
            <a
              href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=31011202022083"
              target="_blank"
              rel="noopener noreferrer"
              >沪公网安备31011202022083号</a
            >
          </p>
        </div>

        <div class="flex flex-wrap gap-6 text-sm">
          <a href="#top" class="hover:text-white">返回顶部</a>
          <a href="#products" class="hover:text-white">产品矩阵</a>
          <a
            href="https://github.com/glosc-ai"
            target="_blank"
            rel="noreferrer"
            class="hover:text-white"
          >
            GitHub
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped></style>
