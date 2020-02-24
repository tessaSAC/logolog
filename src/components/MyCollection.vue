<script>
export default {
  props: {
    logoCollection: {
      type: Object,
      required: true
    }
  },

  methods: {
    removeLogo(logo) { this.$emit('remove-logo', logo) }
  }
}
</script>

<template>
<div class="MyCollection">
  <h1>My Collection</h1>

  <div v-if="!Object.keys(logoCollection).length" class="emptyState">
    <h2 >
      Use the dropdown on the right to start adding to your logo collection.
    </h2>
  </div>

  <div class="logoCollection">
    <div
      v-for="({ logo, name }, domain) in logoCollection"
      :key="domain"
      class="logo"
      role="button"
      @click="removeLogo({ domain, logo, name })"
    >
      <p class="removeLogo">remove</p>
      <img :src="logo" :alt="name" />
    </div>
  </div>
</div>
</template>

<style scoped>
.MyCollection {
  padding: 3rem 4rem;
  max-height: 100%;
}

h1 {
  margin-bottom: 1rem;
  text-align: center;
  font-size: 2rem;
}

.emptyState {
  height: 80%;

  display: flex;
  align-items: center;
  justify-content: center;
}

.emptyState h2 {
  width: 60%;
  max-width: 400px;

  text-align: center;
  font-size: 1.5rem;
  color: #345eab;
}

.logoCollection {
  max-height: calc(100% - 2rem);
  overflow-y: auto;

  display: flex;
  flex-wrap: wrap;
}

.logo {
  cursor: pointer;

  margin: 1rem;
  background: white;
  width: 120px;
  height: 120px;
  filter: drop-shadow(5px 5px 0 var(--colorAccent));

  display: flex;
  align-items: center;
  justify-content: center;
}

.logo:hover {
  position: relative;
  bottom: 4px;
  right: 5px;
  filter: drop-shadow(10px 9px 0 var(--colorAccent));
}

.removeLogo {
  opacity: 0;
  position: absolute;
  top: -2px;

  background: rgba(255, 255, 255, 0.9);
  filter: drop-shadow(2px 2px 0 var(--colorAccent));

  height: 100%;
  width: 100%;

  display: flex;
  justify-content: center;
  align-items: center;

  font-size: 2rem;
  color: var(--colorWarning);
  text-shadow: 2px 2px 0 var(--colorAccentDarker);
}

p.removeLogo:hover { opacity: 1; }

.logo img {
  max-width: 100px;
  max-height: 100px;
}
</style>