<script>
export default {
  props: {
    logoCollection: {
      type: Object,
      required: true,
    },
  },

  data: _ => ({
    searchResults: [],
    searchQuery: '',
  }),

  watch: {
    searchQuery(newQuery) {
      newQuery
        ? this.debouncedSearch()
        : this.searchResults = []
    },
  },

  computed: {
    debouncedSearch() { return this.debounce(this.findLogos, 450) },

    // Don't show already saved logos
    searchResultsFiltered() {
      const logoResults = {}

      this.searchResults.forEach(({ domain, logo, name }) => {
        if(!this.logoCollection[domain]) logoResults[domain] = { logo, name }
      })

      return logoResults
    },
  },

  methods: {
    clearSearch() { this.searchQuery = '' },

    // Create debounced version of any function
    debounce(func, wait) {
      let timeout

      return function() {
        let args = arguments,
            callNow = !timeout,
            context = this,
            later = function() {
              timeout = null
              func.apply(context, args)
            }

        clearTimeout(timeout)
        timeout = setTimeout(later, wait)
      }
    },

    findLogos() {
      fetch(`https://autocomplete.clearbit.com/v1/companies/suggest?query=:${ this.searchQuery }`)
      .then((searchResults) => searchResults.json())
      .then((searchResultsJson) => this.searchResults = searchResultsJson)
    },

    saveLogo(logoSelected) { this.$emit('selected-logo', logoSelected) }
  },
}
</script>

<template>
<div class="AddLogo">

  <label for="logo-search">Add new logo</label>

  <div class="searchBox">
    <p
      v-if="searchQuery"
      class="clearSearchBox"
      role="button"
      @click="clearSearch"
    >x</p>

    <input
      id="logo-search"
      v-model="searchQuery"
      name="logo-search"
      type="text"
    />
  </div>


  <div class="resultsContainer">

    <div
      v-for="(result, domain) in searchResultsFiltered"
      :key="domain"
      class="logoResult"
      role="button"
      @click="saveLogo({ domain, ...result })"
    >
      <img :src="result.logo" :alt="result.name" />

      <p>{{ result.name }}</p>

      <p class="addButton">+</p>

    </div>

  </div>
</div>
</template>

<style scoped>
.AddLogo {
  padding: 3rem 4rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

label {
  margin: 0 0 1rem 1rem;
  align-self: flex-start;
  font-size: 2rem;
}

.searchBox {
  position: relative;
  width: calc(100% - 2rem);
}

.clearSearchBox {
  cursor: pointer;

  position: absolute;
  top: -0.3rem;
  right: 0.6rem;

  font-size: 2rem;
  color: var(--colorWarning);
}

.clearSearchBox:hover {
  top: calc(-0.3rem - 2px);
  right: calc(0.6rem + 2px);
  filter: drop-shadow(2px 2px 0 var(--colorAccent));
}

input {
  margin-bottom: 1rem;
  padding: 0.5rem;
  padding-right: 2rem;

  border: none;
  border-bottom: 4px solid var(--colorAccent);

  width: 100%;
  height: 2rem;

  font-size: 1.5rem;
  font-family: 'VT323', sans-serif;
  color: var(--colorAccentDarker);
}

input:focus {
  outline: none;
  border-bottom: 4px solid var(--colorWarning);
}

.resultsContainer {
  width: 100%;
  max-height: 100%;
  overflow-y: auto;
}

.logoResult {
  cursor: pointer;

  margin: 1rem;
  padding: 1rem 1.5rem;

  background: white;
  max-width: calc(100% - 5px);
  height: 6rem;
  overflow: auto;
  filter: drop-shadow(5px 5px 0 var(--colorAccent));

  display: flex;
  align-content: space-between;
  justify-content: space-between;
  align-items: center;
}

.logoResult:hover {
  filter: drop-shadow(10px 9px 0 var(--colorAccent));

  position: relative;
  bottom: 4px;
  right: 5px;
}

.logoResult:last-child { margin-bottom: 1rem; }

.logoResult img { max-height: 4rem; }

.logoResult p { font-size: 1.4rem; }

.logoResult .addButton {
  font-size: 2rem;
  color: var(--colorAccent);
}

.logoResult:hover .addButton { text-shadow: 1px 2px 0 var(--colorWarning); }
</style>