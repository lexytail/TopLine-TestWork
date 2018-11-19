<template lang="pug">
div
  div.expression
    template(v-for="(fraction, index) in fractions")
      div.field
        calculator-fraction(:fraction="fraction")
      template(v-if="index < fractions.length - 1")
        div.field
          select(v-model="sign[index]").sign
            each sign, index in ['+', '-', '/', '*']
              option #{sign}
    div.field
      div =
    div.field
      calculator-fraction(:readonly="true" :fraction="result")
  div.expression-error {{ error }}
</template>

<script lang="ts">
import { Component, Vue, Prop, Watch } from "nuxt-property-decorator"
import CalculatorFraction, { Fraction } from './fraction.vue'

@Component({
  name: 'calculator-expression',
  components: { CalculatorFraction }
})
export default class extends Vue {

  @Prop()
  public fractions?: Fraction[]

  public result: Fraction = new Fraction

  public sign: string[] = []

  public error: string = ''

  @Watch('sign')
  @Watch('fractions', { deep: true })
  public calculate(fraction: Fraction[]) {

    if (!this.fractions || !this.sign.length) { return }

    try {

      this.result = this.fractions.reduce((fraction, current, index) => {
      
          const sign: string = this.sign[index - 1]

          if (sign === '+') return Fraction.plus(current, fraction)
      
          if (sign === '-') return Fraction.minus(current, fraction)
      
          if (sign === '/') return Fraction.divide(current, fraction)
      
          if (sign === '*') return Fraction.multiply(current, fraction)


        return current

      })

      this.error = ''

    } catch (error) { this.error = error.toString() }


  }

}
</script>

<style lang="stylus" scoped>
.expression
  display flex
  align-items center

  > .field
    padding 0 1rem
    max-width 4rem

</style>