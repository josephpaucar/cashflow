<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action">
      <img
        src="@/assets/trash-icon.svg"
        alt="borrar"
        @click="remove"
      >
      <p
        :class="{'red': isNegative, 'green': !isNegative}"
      >
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { toRefs, defineProps, defineEmits, computed } from 'vue';

const currencyFormater = new Intl.NumberFormat('es-PE', {
  style: 'currency',
  currency: 'PEN'
});

const props = defineProps({
  id: {
    type: Number,
    default: null
  },
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
  amount: {
    type: Number,
    default: 0
  }
});

const { id, title, description, amount } = toRefs(props);

//Computed
const amountCurrency = computed(() => currencyFormater.format(amount.value));
const isNegative = computed(() => amount.value < 0);

const emit = defineEmits(['remove']);

const remove = () => {
  emit('remove', id.value);
};
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 75%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
p {
  font-size: 12px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
    color: red;
}
.green {
    color: green;
}
</style>