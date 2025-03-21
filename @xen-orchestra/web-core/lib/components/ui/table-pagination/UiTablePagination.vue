<!-- v3 -->
<template>
  <div class="ui-table-pagination">
    <div class="buttons-container">
      <PaginationButton :disabled="isFirstPage || disabled" :icon="faAngleDoubleLeft" @click="goToFirstPage()" />
      <PaginationButton :disabled="isFirstPage || disabled" :icon="faAngleLeft" @click="goToPreviousPage()" />
      <PaginationButton :disabled="isLastPage || disabled" :icon="faAngleRight" @click="goToNextPage()" />
      <PaginationButton :disabled="isLastPage || disabled" :icon="faAngleDoubleRight" @click="goToLastPage()" />
    </div>
    <span class="typo-body-regular-small label">
      {{ $t('core.select.n-object-of', { from: startIndex, to: endIndex, total: totalItems }) }}
    </span>
    <span class="typo-body-regular-small label show">{{ $t('core.show-by') }}</span>
    <div class="dropdown-wrapper">
      <select v-model="pageSize" :disabled class="dropdown typo-body-regular-small" @change="goToFirstPage">
        <option v-for="option in pageSizeOptions" :key="option" :value="option" class="typo-body-bold-small">
          {{ option }}
        </option>
      </select>
      <VtsIcon class="icon" accent="current" :icon="faAngleDown" />
    </div>
  </div>
</template>

<script setup lang="ts">
import VtsIcon from '@core/components/icon/VtsIcon.vue'
import PaginationButton from '@core/components/ui/table-pagination/PaginationButton.vue'
import {
  faAngleDoubleLeft,
  faAngleDoubleRight,
  faAngleDown,
  faAngleLeft,
  faAngleRight,
} from '@fortawesome/free-solid-svg-icons'
import { useOffsetPagination } from '@vueuse/core'
import { computed, ref, watch } from 'vue'

export type PaginationPayload = {
  currentPage: number
  pageSize: number
  startIndex: number
  endIndex: number
}

const { totalItems, disabled = false } = defineProps<{
  totalItems: number
  disabled?: boolean
}>()

const emit = defineEmits<{
  change: [payload: PaginationPayload]
}>()

const pageSize = ref(50)
const pageSizeOptions = [10, 50, 100, 150, 200]
const {
  currentPage,
  currentPageSize,
  pageCount,
  isFirstPage,
  isLastPage,
  prev: goToPreviousPage,
  next: goToNextPage,
} = useOffsetPagination({
  total: () => totalItems,
  pageSize,
})
const startIndex = computed(() => (currentPage.value - 1) * currentPageSize.value + 1)
const endIndex = computed(() => Math.min(currentPage.value * currentPageSize.value, totalItems))

const goToFirstPage = () => {
  currentPage.value = 1
}
const goToLastPage = () => {
  currentPage.value = pageCount.value
}

watch([currentPage, currentPageSize], ([newPage, newPageSize]) => {
  emit('change', {
    currentPage: newPage,
    pageSize: newPageSize,
    startIndex: startIndex.value,
    endIndex: endIndex.value,
  })
})
</script>

<style scoped lang="postcss">
.ui-table-pagination {
  display: flex;
  align-items: center;
  gap: 0.8rem;

  .buttons-container {
    display: flex;
    gap: 0.2rem;
  }

  .label {
    color: var(--color-neutral-txt-secondary);
  }

  .show::before {
    content: '-';
    margin-right: 0.8rem;
  }

  .dropdown-wrapper {
    position: relative;

    .dropdown {
      cursor: pointer;
      padding: 0.2rem 0.6rem;
      height: 3rem;
      width: 5rem;
      appearance: none;
      border-radius: 0.4rem;
      color: var(--color-brand-txt-base);
      border: 0.1rem solid var(--color-neutral-border);
      background-color: var(--color-neutral-background-primary);

      &:hover {
        border-color: var(--color-brand-item-hover);
        background-color: var(--color-brand-background-hover);
        color: var(--color-brand-txt-hover);

        + .icon {
          color: var(--color-brand-txt-hover);
        }
      }

      &:disabled {
        cursor: not-allowed;
        background-color: var(--color-neutral-background-disabled);
        color: var(--color-neutral-txt-secondary);
        border-color: transparent;

        + .icon {
          color: var(--color-neutral-txt-secondary);
        }
      }

      &:active {
        background-color: var(--color-brand-background-active);
        border-color: var(--color-brand-item-active);
      }

      &:focus-visible {
        outline: 0.1rem solid var(--color-brand-item-base);
        border: 0.1rem solid var(--color-brand-item-base);
        color: var(--color-brand-txt-base);
        background-color: var(--color-brand-background-selected);

        + .icon {
          color: var(--color-brand-txt-base);
        }
      }

      option {
        background-color: var(--color-neutral-background-primary);
        border: 0.1rem solid var(--color-neutral-border);
        border-radius: 0.4rem;
        color: var(--color-neutral-txt-primary);
      }
    }

    .icon {
      position: absolute;
      top: 50%;
      right: 0.8rem;
      transform: translateY(-50%);
      pointer-events: none;
      font-size: 1rem;
      color: var(--color-brand-txt-base);
    }
  }
}
</style>
