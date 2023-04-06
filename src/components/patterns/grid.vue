<template>
    <svg id="grid" viewBox="0 0 222 222" xmlns="http://www.w3.org/2000/svg" className="">
      <defs>
        <pattern
          id="svg-pattern-grid"
          x="0"
          y="0"
          width="44"
          height="44"
          patternUnits="userSpaceOnUse"
          patternTransform="translate(1, 1)  skewX(0)"
        >
          <svg width="43" height="43" viewBox="0 0 100 100">
            <g fill="#ffffff" opacity="1" >
              <rect width="100" height="100"></rect>
            </g>
          </svg>
        </pattern>
      </defs>
      <rect x="0" y="0" width="100%" height="100%" fill="#000000" :fill-opacity="opacity"></rect>
      <rect
        x="0"
        y="0"
        width="100%"
        height="100%"
        fill="url(#svg-pattern-grid)"
        :fill-opacity="opacity"
      ></rect>
    </svg>
</template>

<script>
export default {
   name: 'GridPattern',
}
</script>

<style scoped>
/* rect {
	mix-blend-mode: soft-light;
} */
</style>