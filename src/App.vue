<script>
import AddLogo from './components/AddLogo'
import MyCollection from './components/MyCollection'
import TopNav from './components/TopNav'

export default {
  name: "App",

  components: {
    AddLogo,
    MyCollection,
    TopNav
  },

  data: _ => ({ logoCollection: {} }),

  methods: {
    removeLogo({ domain, logo, name }) {
      if(!this.logoCollection[domain]) return

      const newCollection = {}

      for(const [savedDomain, savedLogo] of Object.entries(this.logoCollection)) {
        if(domain !== savedDomain) newCollection[savedDomain] = savedLogo
      }

      this.logoCollection = newCollection
    },

    saveLogo({ domain, logo, name }) {
      if(!this.logoCollection[domain]) this.$set(this.logoCollection, domain, { logo, name })
    }
  },
}
</script>

<template>
<div id="app">

  <TopNav />

  <div class="mainContent">

    <AddLogo
      :logoCollection="logoCollection"
      @selected-logo="saveLogo"
    />

    <MyCollection
      :logoCollection="logoCollection"
      @remove-logo="removeLogo"
    />

  </div>
</div>
</template>


<style>
body {
  --colorAccent: #4444dd;
  --colorAccentDarker: #244e9a;
  --colorMain: cornflowerblue;
  --colorMainDarker: #638edc;
  --colorWarning: #ff00b3;
}


.TopNav {
  background: var(--colorAccentDarker);
  height: 50px;
}

.mainContent {
  display: flex;
  width: 100vw;
  height: calc(100vh - 50px);
}

.AddLogo {
  border-right: 6px solid var(--colorAccent);
  background: var(--colorMain);
  width: 40vw;
}

.MyCollection {
  background: var(--colorMainDarker);
  width: 60vw;
}



/* apply a natural box layout model to all elements, but allowing components to change */
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}

/* http://meyerweb.com/eric/tools/css/reset/
   v2.0 | 20110126
   License: none (public domain)
*/
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 16px;
	font-family: 'VT323', sans-serif;
  color: var(--colorAccentDarker);
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
</style>
