<template>
  <div
    class="bg-light-layer-0 text-light-text dark:bg-dark-layer-0 dark:text-dark-text"
  >
    <Head>
      <Title>{{ $t("_global.legal") }}</Title>
    </Head>
    <div class="bg-light-layer-1 dark:bg-dark-layer-1">
      <div class="responsive-py-4 responsive-px-5 flex w-full flex-col">
        <HeaderAppPage
          :header="$t('_global.legal')"
          :tagline="$t('pages.legal.index.subheader')"
        />
      </div>
    </div>
    <div class="responsive-py-5 responsive-px-5">
      <h3 class="responsive-h2 transition-all duration-500">
        {{ $t("pages.legal.index.section_1_subheader") }}
      </h3>
      <p
        class="responsive-py-1 text-light-distinct-text dark:text-dark-distinct-text"
      >
        {{ $t("pages.legal.index.section_1_tagline") }}
      </p>
      <GridDocEntries class="responsive-py-1" :cards="cards" />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { DocsEntry } from "~/types/docs-entry";

const cards: DocsEntry[] = [
  {
    id: 1,
    url: "trademark-policy",
    title: "_global.trademark_policy",
    description: "pages.legal.index.trademark_policy_description",
    imgURL: `${BOOTSTRAP_TRADEMARK_URL}`,
    imgDimensions: "h-16 sm:h-20",
    imgAltText: "pages.legal._global.trademark_policy_alt_text",
  },
  {
    id: 2,
    url: "privacy-policy",
    title: "_global.privacy_policy",
    description: "pages.legal.index.privacy_policy_description",
    imgURL: `${BOOTSTRAP_SHIELD_CHECK_URL}`,
    imgDimensions: "h-16 sm:h-20",
    imgAltText: "pages.legal._global.privacy_policy_alt_text",
  },
];
</script>
