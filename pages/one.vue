<template lang="pug">
.page
  h1 Калькулятор дробей
  calculator-expression(:fractions="fractions")
  button(@click="addFraction") Add Fraction
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import CalculatorExpression from '~/components/calculator/expression.vue'
import { Fraction } from '~/components/calculator/fraction.vue'

@Component({
  components: { CalculatorExpression }
})
export default class extends Vue {

  public fractions: Fraction[] = [new Fraction, new Fraction]

  public addFraction() {

    this.fractions.push(new Fraction)

  }

}
</script>