<template lang="pug">
.fraction
  input(type="number" v-model.number="fraction.numerator", :readonly="readonly").numerator
  hr
  input(type="number" v-model.number="fraction.denominator", :readonly="readonly").denominator
</template>

<script lang="ts">
import { Component, Vue, Prop } from "nuxt-property-decorator"

@Component({ name: 'calculator-fraction' })
export default class extends Vue {

  @Prop()
  public readonly?: boolean

  @Prop()
  public fraction?: Fraction

}

export class Fraction {

  constructor(

    public numerator: number = 1,

    public denominator: number = 1

  ) {

    if (denominator === 0) throw Error('Denominator !== 0')

  }

  get value(): number {

    return this.numerator / this.denominator

  }

  public static plus(fraction1: Fraction, fraction2: Fraction): Fraction {

    let numerator: number = (fraction1.numerator * fraction2.denominator) + (fraction2.numerator * fraction1.denominator)

    let denominator: number = fraction1.denominator * fraction2.denominator

    const fraction = new Fraction(numerator, denominator)

    // Fraction.reduce(fraction)

    return fraction

  }

  public static minus(fraction1: Fraction, fraction2: Fraction): Fraction {

    let numerator: number = (fraction1.numerator * fraction2.denominator) - (fraction2.numerator * fraction1.denominator)

    let denominator: number = fraction1.denominator * fraction2.denominator

    const fraction = new Fraction(numerator, denominator)

    // Fraction.reduce(fraction)

    return fraction

  }

  public static divide(farction1: Fraction, fraction2: Fraction): Fraction {

    let numerator: number = farction1.numerator * fraction2.denominator

    let denominator: number = farction1.denominator * fraction2.numerator

    const fraction = new Fraction(numerator, denominator)

    // Fraction.reduce(fraction)

    return fraction

  }

  public static multiply(farction1: Fraction, fraction2: Fraction): Fraction {

    let numerator: number = farction1.numerator * fraction2.numerator

    let denominator: number = farction1.denominator * fraction2.denominator

    const fraction = new Fraction(numerator, denominator)

    // Fraction.reduce(fraction)

    return fraction

  }

  public static reduce(fraction: Fraction) {

    if (fraction.numerator % 2 === 0 && fraction.denominator % 2 === 0) {

      fraction.numerator /= 2

      fraction.denominator /= 2

    }

    if (fraction.numerator % fraction.denominator === 0) {

      fraction.numerator /= fraction.denominator

    }

  }

}
</script>

<style lang="stylus" scoped>
.numerator, .denominator
  border 1px #d2d0d0 solid
  border-radius 2px
  box-shadow 0 2px 11px -7px inset
  color #565c65
  font-size 20px
  height 30px
  max-width 100%
  text-align center
</style>