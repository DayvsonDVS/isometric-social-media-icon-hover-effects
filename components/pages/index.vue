<template>
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.2/font/bootstrap-icons.css"
    integrity="sha384-b6lVK+yci+bfDmaY1u0zE8YYJt0TZxLEAFyYSLHId4xoVvsrQu3INevFKo+Xir8e"
    crossorigin="anonymous"
  />
  <ul>
    <li v-for="{ icon } in list">
      <a href="#">
        <span></span>
        <span></span>
        <span></span>
        <span></span>
        <span :class="`bi bi-${icon}`"></span>
      </a>
    </li>
  </ul>
</template>

<script setup lang="ts">
import '/assets/scss/main.scss'

const list = [
  { icon: 'facebook' },
  { icon: 'twitter' },
  { icon: 'whatsapp' },
  { icon: 'linkedin' },
  { icon: 'instagram' }
]
</script>

<style scoped lang="scss">
$colors: facebook, twitter, whatsapp, linkedin, instagram;
$index: 1, 2, 3, 4, 5;
ul {
  position: relative;
  display: flex;
  transform-style: preserve-3d;
  transform: rotate(-25deg) skew(25deg);
  li {
    position: relative;
    list-style: none;
    width: 60px;
    height: 60px;
    margin: 0 10px;
    &::before {
      position: absolute;
      content: '';
      bottom: -10px;
      left: 0;
      width: 100%;
      height: 10px;
      background: #2a2a2a;
      transform-origin: top;
      transform: skewX(-41deg);
    }
    &::after {
      position: absolute;
      content: '';
      top: 0;
      left: -9px;
      width: 9px;
      height: 100%;
      background: #2a2a2a;
      transform-origin: right;
      transform: skewy(-49deg);
    }
    @each $color in $colors {
      $i: index($colors, $color);
      &:nth-child(#{$i}):hover {
        span {
          background: var(--color-#{$color}, $i);
        }
      }
    }
    :hover {
      span {
        z-index: 1000;
        transition: 0.5s;
        color: #fff;
        box-shadow: -1px 1px 1px rgba(0, 0, 0, 0.05);
        @each $i in 5, 4, 3, 2, 1 {
          &:nth-child(#{$i}) {
            @if $i == 5 {
              transform: translate(($i - 1) * 10 + px, (-$i + 1) * 10 + px);
              opacity: 1;
            } @else if $i != 1 {
              transform: translate(($i - 1) * 10 + px, (-$i + 1) * 10 + px);
              opacity: calc(($i * 2) / 10);
            } @else {
              transform: translate(0px, 0px);
              opacity: 0.2;
            }
          }
        }
      }
    }
    span {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex !important;
      justify-content: center;
      align-items: center;
      background: #333;
      color: rgba(255, 255, 255, 0.2);
      font-size: 30px !important;
      transition: 0.2s;
      z-index: 1;
    }
  }
}
</style>
