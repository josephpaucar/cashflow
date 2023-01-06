<template>
  <main>
    <p>{{ selectedDate }}</p>
    <h1>{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic" />
    </div>
    <div class="action">
      <slot name="action" />
    </div>
  </main>
</template>

<script>
const currencyFormater = new Intl.NumberFormat('es-PE', {
  style: 'currency',
  currency: 'PEN'
});

export default {
  props: {
    label: {
      type: String,
      required: true
    },
    date: {
      type: String,
      default: null
    },
    amount: {
      type: Number,
      default: 0
    },
    totalAmount: {
      type: Number,
      default: 0
    }
  },
  computed: {
    amountVisual() {
      return this.amount !== null ? this.amount : this.totalAmount;
    },
    selectedDate() {
      return this.date !== null ? this.date : this.label;
    },
    amountCurrency() {
      return currencyFormater.format(this.amountVisual);
    }
  },  
};
</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>