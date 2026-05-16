<script setup lang="ts">
import { useI18n } from '../composables/useI18n'
import { computed } from 'vue'

const { locale } = useI18n()

const isEn = computed(() => locale.value === 'en')
</script>

<template>
  <article class="py-32 bg-bg-primary min-h-screen">
    <div class="max-w-3xl mx-auto px-6 rules-content">

      <!-- Back link -->
      <router-link to="/" class="inline-flex items-center gap-2 text-text-tertiary hover:text-text-primary transition-colors mb-12">
        <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" /></svg>
        {{ isEn ? 'Back to Home' : '返回首页' }}
      </router-link>

      <template v-if="isEn">
        <h1 class="heading-serif text-4xl md:text-5xl text-text-primary mb-4">Official Rules</h1>
        <p class="text-text-tertiary mb-4">[EVENT_NAME]</p>
        <p class="text-text-tertiary/60 text-sm mb-12">Draft, subject to change</p>

        <hr class="border-border mb-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">1. Overview</h2>
        <p>[EVENT_NAME] is a hackathon organized by [ORGANIZER].</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">2. Event Scope</h2>
        <p>Planned venue: <strong>[VENUE], [CITY]</strong>.</p>
        <p>The detailed schedule will be announced by the organizer separately.</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">3. Eligibility</h2>
        <p>Participants must satisfy all of the following requirements:</p>
        <ul>
          <li>Be legally able to participate in a skills-based competition under the laws of their local jurisdiction</li>
          <li>Register using accurate and complete information</li>
          <li>Agree to these rules and any additional event instructions published by the organizer</li>
          <li>Participate as an individual or as part of only one team</li>
        </ul>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">4. Team Rules</h2>
        <ul>
          <li>Participants may join as an individual or form a team</li>
          <li>Each team may have up to <strong>3</strong> members</li>
          <li>A participant may belong to only <strong>1</strong> team</li>
          <li>Each team may submit only <strong>1</strong> project</li>
        </ul>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">5. Submission Requirements</h2>
        <p>Each team must submit a complete project package before the official deadline. A valid submission should include:</p>
        <ul>
          <li>Project name and team information</li>
          <li>A short project description</li>
          <li>A demo link or working artifact</li>
          <li>Source repository link</li>
          <li>A demo video (3-5 minutes recommended)</li>
        </ul>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">6. Judging Criteria</h2>
        <p>Each dimension counts for <strong>20%</strong> of the total score: Innovation, Technical Depth, Completeness, Practicality, Presentation.</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">7. Code of Conduct</h2>
        <p>All participants are expected to behave professionally and respectfully. Harassment, discrimination, and disruptive conduct will not be tolerated.</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">8. Intellectual Property</h2>
        <p>Participants retain ownership of the intellectual property in the projects they create.</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">9. Contact</h2>
        <p>Questions should be directed to the official hackathon contact channels.</p>

      </template>

      <template v-else>
        <h1 class="heading-serif text-4xl md:text-5xl text-text-primary mb-4">官方规则</h1>
        <p class="text-text-tertiary mb-4">[EVENT_NAME]</p>
        <p class="text-text-tertiary/60 text-sm mb-12">草案，可能会有调整</p>

        <hr class="border-border mb-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">1. 概述</h2>
        <p>[EVENT_NAME] 是由 [ORGANIZER] 组织的黑客松。</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">2. 参赛资格</h2>
        <p>参赛者必须满足以下条件：使用准确完整的信息注册，同意本规则，以个人或团队成员身份参赛。</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">3. 团队规则</h2>
        <ul>
          <li>每个团队最多 <strong>3</strong> 名成员</li>
          <li>每位参赛者只能加入 <strong>1</strong> 个团队</li>
          <li>每个团队只能提交 <strong>1</strong> 个项目</li>
        </ul>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">4. 行为准则</h2>
        <p>所有参赛者都应表现出专业和尊重。</p>

        <hr class="border-border my-12" />

        <h2 class="heading-serif text-2xl text-text-primary mb-6">5. 联系方式</h2>
        <p>请通过官方联系渠道进行咨询。</p>

      </template>

    </div>
  </article>
</template>

<style scoped>
.rules-content p {
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: 1rem;
}

.rules-content ul {
  list-style: disc;
  padding-left: 1.5rem;
  margin-bottom: 1rem;
}

.rules-content li {
  color: var(--color-text-secondary);
  line-height: 1.8;
  margin-bottom: 0.5rem;
}

.rules-content a {
  color: var(--color-accent-blue, #3BA7D0);
}
</style>
