<template>
  <div id="search-app">
    <Nuxt keep-alive />
  </div>
</template>

<style>
html {
  font-family: Consolas, 'Andale Mono WT', 'Andale Mono', 'Lucida Console',
    'Lucida Sans Typewriter', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono',
    'Liberation Mono', 'Nimbus Mono L', Monaco, 'Courier New', Courier,
    monospace;
  font-size: 1rem;
  line-height: 1.5;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;

  --accent-color: #f44046;
  --background-color: #0e141b;
  --accent-color--alt: #4e40f4;
  --font-primary: white;
  --link-color: var(--font-primary);
  --visited-link-color: var(--accent-color);
  background: var(--background-color);
  color: var(--font-primary);
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
label {
  margin-bottom: 1rem;
}
input {
  padding: 0.5rem;
  font-size: 1rem;
  color: var(--background-color);
  border: 1px solid var(--font-primary);
}

input:focus {
  outline: 0;
  border-color: var(--accent-color);
}

input[type='submit'] {
  color: var(--font-primary);
  background: var(--accent-color);
  border: 1px solid var(--accent-color);
}

a {
  color: var(--link-color);
}
a:visited {
  color: var(--visited-link-color);
}

#search-app {
  margin: 0 5rem;
}

@media only screen and (max-width: 600px) {
  #search-app {
    margin: 0;
  }
}
</style>
