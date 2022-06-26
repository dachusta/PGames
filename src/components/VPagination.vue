<template>
  <div class="pagination">
    <!-- :disabled="currentPage <= 1" -->
    <button
      class="btn-page previous"
      @click="gotoPage(currentPage - 1)"
    >
      prev
    </button>

    <button
      class="btn-page"
      :class="{ active: currentPage }"
    >
      {{ currentPage }}
    </button>

    <!-- <button
      v-if="orderPage(1) >= 1"
      class="btn-page"
      :class="{ active: currentPage === orderPage(1) }"
      @click="gotoPage(orderPage(1))"
    >
      {{ orderPage(1) }}
    </button>

    <button
      v-if="orderPage(2) >= 2"
      class="btn-page"
      :class="{ active: currentPage === orderPage(2) }"
      @click="gotoPage(orderPage(2))"
    >
      {{ orderPage(2) }}
    </button>
    <span
      v-else-if="orderPage(2) === '...'"
      class="gap-page"
    >...</span>

    <button
      v-if="orderPage(3) >= 3"
      class="btn-page"
      :class="{ active: currentPage === orderPage(3) }"
      @click="gotoPage(orderPage(3))"
    >
      {{ orderPage(3) }}
    </button>

    <button
      v-if="orderPage(4) >= 4"
      class="btn-page"
      :class="{ active: currentPage === orderPage(4) }"
      @click="gotoPage(orderPage(4))"
    >
      {{ orderPage(4) }}
    </button>

    <button
      v-if="orderPage(5) >= 5"
      class="btn-page"
      :class="{ active: currentPage === orderPage(5) }"
      @click="gotoPage(orderPage(5))"
    >
      {{ orderPage(5) }}
    </button>

    <button
      v-if="orderPage(6) >= 6"
      class="btn-page"
      :class="{ active: currentPage === orderPage(6) }"
      @click="gotoPage(orderPage(6))"
    >
      {{ orderPage(6) }}
    </button>
    <span
      v-else-if="orderPage(2) === '...'"
      class="gap-page"
    >...</span>

    <button
      v-if="orderPage(7) >= 7"
      class="btn-page"
      :class="{ active: currentPage === orderPage(7) }"
      @click="gotoPage(orderPage(7))"
    >
      {{ orderPage(7) }}
    </button> -->

    <!-- :disabled="totalPage <= currentPage" -->
    <button
      class="btn-page next"
      @click="gotoPage(currentPage + 1)"
    >
      next
    </button>

    <!-- <div class="pagination__show">
      <span>Show:</span>
      <select
        :key="show"
        class="pagination__show-select top-options default"
        :options="showList"
        :placeholder="show"
        @selected="selectedShow"
      />
      <span>{{ totalItems }}</span>
    </div> -->
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'

// eslint-disable-next-line
const props = defineProps({
  list: {
    type: Array,
    default () {
      return []
    }
  },
  showList: {
    type: Array,
    default () {
      return [10, 25, 50, 100, 200]
    }
  }
})

// eslint-disable-next-line
const emit = defineEmits(['visibleList', 'setCurrentPage'])

const show = ref(25)

const currentPage = ref(1)

// const totalItems = computed(() => props.list?.length || 0)

// const totalPage = computed(
//   () => props.list?.length
//     ? Math.ceil(props.list?.length / show.value)
//     : 0
// )

const visibleList = computed(() => {
  if (props.list?.length) {
    const begin = show.value * currentPage.value - show.value
    const end = show.value * currentPage.value
    const visibleList = props.list.slice(begin, end)

    return visibleList
  } else return 0
})

watch(() => props.list, () => {
  emit('visibleList', visibleList)
})
watch(() => currentPage.value, () => {
  emit('visibleList', visibleList)
  console.log(currentPage.value)
  emit('setCurrentPage', currentPage.value)
})
watch(() => show, () => {
  emit('visibleList', visibleList)
})

// const selectedShow = (value) => {
//   show.value = value
// }

// Order to number page
// const orderPage = (index) => {
//   switch (index) {
//     case 1:
//       return 1
//     case 2:
//       if (
//         (currentPage.value <= 3 && totalPage.value >= 2) ||
//         (totalPage.value <= 7 && totalPage.value >= 2)
//       ) return 2
//       else if (currentPage.value <= 1) return currentPage.value
//       else return '...'
//     case 3:
//       if (
//         (currentPage.value <= 3 && totalPage.value >= 3) ||
//         (totalPage.value <= 7 && totalPage.value >= 3)
//       ) return 3
//       else if (totalPage.value - 4 >= currentPage.value) return currentPage.value
//       else return totalPage.value - 4
//     case 4:
//       if (
//         (currentPage.value <= 3 && totalPage.value >= 4) ||
//         (totalPage.value <= 7 && totalPage.value >= 4)
//       ) return 4
//       else if (totalPage.value - 4 >= currentPage.value) return currentPage.value + 1
//       else return totalPage.value - 3
//     case 5:
//       if (
//         (currentPage.value <= 3 && totalPage.value >= 5) ||
//         (totalPage.value <= 7 && totalPage.value >= 5)
//       ) return 5
//       else if (totalPage.value - 4 >= currentPage.value) return currentPage.value + 2
//       else return totalPage.value - 2
//     case 6:
//       if (totalPage.value - 4 <= currentPage.value || totalPage.value <= 7) return totalPage.value - 1
//       else return '...'
//     case 7:
//       return totalPage.value
//     default:
//       return 1
//   }
// }
const gotoPage = (numberPage) => {
  currentPage.value = numberPage
}
</script>

<style lang="scss" scoped>
.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0px 10px;
  margin: 30px auto 0px auto;
  padding: 5px 100px;
  font-size: 14px;
  background: #3c4464;
  border-radius: 10px;
  box-shadow: 1px 1px 3px 0px rgba(0, 0, 0, 0.15);
}
.btn-page {
  width: 40px;
  height: 30px;
  padding: 0;
  border: 1px solid #000000;
  background: #1C1C2C;
  color: #ffffff;
  cursor: pointer;

  &.active {
    background: #63a3ec;
    color: #ffffff;
  }

  &:disabled {
    cursor: default;
    opacity: 0.5;
  }
}

.gap-page {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 30px;
  font-size: 18px;
  letter-spacing: 3px;
  cursor: default;
  user-select: none;
}

.icon-previous,
.icon-next {
  width: 10px;
  height: 10px;
}

.pagination__show {
  display: flex;
  align-items: center;
  gap: 5px;
  padding-left: 10px;
}

</style>
