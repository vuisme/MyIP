<template>
  <footer>
    <div id="copyleft">
      <p class="text-center">{{ $t('page.footerName') }} <a :href="$t('page.footerLink')" class="link-dark"
          target="_blank" @click="$trackEvent('Footer', 'FooterClick', 'Github');" aria-label="Github"><i
            class="bi bi-github" :class="{ 'dark-mode': isDarkMode }"
            v-tooltip="{ title: $t('Tooltips.GithubLink'), placement: 'top' }"></i></a>
      </p>
    </div>

    <div id="copyright" v-if="!configs.originalSite">
      <p class="text-center fs-6 fw-light" style="opacity: 0.5;">
        {{ $t('page.copyRightName') }} <a :href="$t('page.copyRightLink')" class="link-underline-light" target="_blank"
          :class="[isDarkMode ? 'dark-mode link-light' : 'link-dark']">{{ $t('page.copyRightLinkName') }}</a>
      </p>
    </div>
  </footer>
</template>

<script>
import { ref, computed, watch } from 'vue';
import { useStore } from 'vuex';
import '@khmyznikov/pwa-install';

export default {
  name: 'Footer',

  // 引入 Store
  setup() {
    const store = useStore();
    const isDarkMode = computed(() => store.state.isDarkMode);
    const isMobile = computed(() => store.state.isMobile);
    const configs = computed(() => store.state.configs);

    return {
      isDarkMode,
      isMobile,
      configs,
    };
  },

  data() {
    return {
      showAbout: true,
      showChanglog: false,
      changelog: this.$tm('changelog.versions'),
    }
  },
  methods: {
    toggleContent(contentType) {
      this.showAbout = contentType === 'about';
      this.showChanglog = contentType === 'changlog';
      this.$refs.offcanvasBody.scrollTop = 0;
    },
  },
}
</script>

<style scoped>
#About {
  z-index: 1051;
}
</style>
