<template lang="pug">
  article.row.card.o-card.mb-40.u-no-nest
    .column.small-12.medium-3.large-12.align-middle
      icon.card__icon.c-ship-gray-25(:type="iconType")
    .card__content.column.small-12.medium-9.large-12
      h3.card__title.o-heading-3.c-ship-gray {{ $t(title) }}
      p.card__desc.o-paragraph.c-ship-gray-40(:class="{ 'mb-24': ctaTo }") {{ $t(desc) }}
      a.card__to.o-btn(
        v-if="ctaTo && useNativeATag"
        :href="ctaTo",
        :class="`o-btn--${color}`",
      )
        span.c-white.fs-16 {{ $t(ctaText) }}
      router-link.card__to.o-btn(
        v-if="ctaTo && !useNativeATag"
        :to="ctaTo",
        :class="`o-btn--${color}`",
      )
        span.c-white.fs-16 {{ $t(ctaText) }}
      button.card__contact.o-link(
        type="button",
        v-if="contactUs",
        @click="openContactModal()",
        :class="`c-${color}`",
      ) {{ $t('common.orContactUs') }}
</template>

<script>
  import { openContactModal } from 'services/events'

  export default {
    props: {
      iconType: {
        type: String,
        required: true,
      },
      title: {
        type: String,
        required: true,
      },
      desc: {
        type: String,
        required: true,
      },
      ctaTo: {
        type: [Object, String],
        required: false,
      },
      ctaText: {
        type: String,
        required: false,
      },
      contactUs: {
        type: Boolean,
        default: true,
      },
      color: {
        type: String,
        required: false,
      },
    },
    computed: {
      useNativeATag() {
        return typeof this.ctaTo === 'string'
      },
    },
    methods: {
      openContactModal,
    },
  }
</script>

<style src="./Card.sass" lang="sass" scoped></style>
