<template>
  <form action="/search" method="get">
    <label for="search">Search Github Users</label>
    <span>
      <input
        id="search"
        type="text"
        aria-label="Search Github Users"
        name="q"
        placeholder="znapfel"
      />
      <input type="submit" value="Search" />
    </span>
  </form>
</template>

<style>
form {
  display: flex;
  flex-direction: column;
}

form label {
  text-align: center;
}
form span {
  display: flex;
  justify-content: center;
}

form input[type='text'] {
  border-top-left-radius: 1rem;
  border-bottom-left-radius: 1rem;
}

form input[type='submit'] {
  border-top-right-radius: 1rem;
  border-bottom-right-radius: 1rem;
}

@media only screen and (max-width: 300px) {
  form {
    flex-direction: column;
  }
}
</style>
