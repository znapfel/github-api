a
<template>
  <div v-if="$fetchState.pending" class=""></div>
  <p v-else-if="$fetchState.error">{{ $fetchState.error }}</p>
  <div v-else class="user-profile">
    <div v-if="loaded" class="user-info">
      <div class="user-bio">
        <h3>
          <a
            class="card-link"
            :href="userData.html_url"
            :alt="userData.login"
            >{{ userData.login }}</a
          >
        </h3>
        <p>{{ userData.bio }}</p>
      </div>
      <a
        class="image-container card-link"
        :href="userData.html_url"
        :alt="userData.login"
        ><img :src="userData.avatar_url"
      /></a>
    </div>
    <div class="user-stats">
      <div v-if="userData.public_repos" class="stat">
        <span>{{ userData.public_repos }}</span> repos
      </div>
      <div v-if="userData.followers" class="stat">
        <span>{{ userData.followers }}</span> followers
      </div>
      <div v-if="userData.public_gists" class="stat">
        <span>{{ userData.public_gists }}</span> gists
      </div>
    </div>
    <!-- <pre>{{ userData }}</pre> -->
  </div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  data() {
    return {
      userData: {},
      loaded: false,
    }
  },
  async fetch() {
    const headers = {
      // eslint-disable-next-line prettier/prettier
      Authorization: `${this.$config.githubToken}`,
    }
    console.log({ headers })

    this.userData = await fetch(
      `https://api.github.com/users/${this.user.login}`,
      {
        headers,
      }
    ).then((res) => res.json())
    console.log({ data: this.userData })

    this.loaded = true
  },
}
</script>

<style>
img {
  width: 5rem;
  border-radius: 1rem;

  border-bottom: 5px solid var(--accent-color--alt);
}

.profile-loading {
  height: 165px;
}

.user-profile {
  background: var(--font-primary);
  color: var(--background-color);
  border-bottom: 5px solid var(--accent-color);
  padding: 2rem;
  margin: 2rem;
  border-radius: 1rem;
}

.card-link {
  color: var(--background-color);
}

.user-info {
  display: grid;
  grid-template-columns: 4fr 1fr;
}

.user-info p {
  font-size: 0.9rem;
  padding-right: 2rem;
}

.user-stats {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  margin-top: 0.5rem;
}

.stat {
  display: flex;
  flex-direction: column;
}

.stat span {
  color: var(--accent-color);
  font-weight: 700;
}

@media only screen and (max-width: 600px) {
  .user-profile {
    min-width: 9rem;
  }
  .user-info {
    grid-template-columns: 1fr;
    grid-template-rows: 1fr;
  }

  .user-info .image-container {
    grid-row: 1;
  }

  .user-stats {
    grid-template-columns: 1fr;
    grid-template-rows: 1fr;
  }

  .stat {
    margin-bottom: 2rem;
    grid-row: 1fr 1fr 1fr;
  }
}
</style>
