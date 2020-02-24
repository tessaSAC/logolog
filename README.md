# logolog
*Visual logo library application using [Clearbit autocomplete logo API](https://clearbit.com/docs?javascript#autocomplete-api).
(Catalyst front-end challenge)*
[ 
### [[ view deployed application ]](https://logolog.netlify.com)

## Approach
1. Review requirements
1. Thumbnail potential layout ideas
1. Get Clearbit API working
1. Create rough search functionality
1. Break out component files for nav, search, and selected icons
1. Create filter functionalities (to save logos and filter out saved logos from results)
1. Break up app into components
1. Ensure state is reactive across all components
1. Style
1. Deploy

## Issues
1. Sass was not working (seems to be an issue with Webpack, may be related to below)
1. Seems to be an issue with UglifyJs; briefly looked into solutions such as [1](https://forum.vuejs.org/t/unexpected-token-operator-from-uglifyjs/10848) [2](https://stackoverflow.com/questions/43888474/unexpected-token-operator-from-uglifyjs) [3](https://github.com/webpack-contrib/uglifyjs-webpack-plugin/issues/112#issuecomment-329069520) [4](https://github.com/webpack-contrib/uglifyjs-webpack-plugin/issues/144)

## Other thoughts
- Wasn't sure if "autocomplete" referred to search input behavior (based on wireframes I'm guessing no) or specific Clearbit API
- Without a link was not 100% clear on which API to use
- Considered porting to Vue CLI 3+ project
