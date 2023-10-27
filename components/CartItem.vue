<template>
  <div class="flex justify-start my-2">

  </div>
</template>
<script setup>
import { useUserStore } from '~/stores/user';


const props = defineProps(['products', 'selectedArray'])
const {product, selectedArray} = toRefs(props)

const emit=defineEmits(['selectedRadio'])
let isHover = ref(false)
let isSelected = ref(false)
const userStore = useUserStore()

const removeFromCart = () => {
  userStore.cart.forEach((prod, index) => {
    if (prod.id === product.value.id) {
      userStore.cart.splice(index, 1)
    }
  })
}

watch(() => isSelected.value, (val) => {
  emit('selectedRadio', { id: product.value.id, val})
})

</script>