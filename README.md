# MilNode Charts package project

MilNode Charts is a collection of data used to make beautiful charts based on Highcharts. MilNode Charts provides the following features:
- Light/Dark theme for charts

MilNode works well with MilNode plugin. See MilNode documentation to know how to use MilNode template, with the following main features:
- Localization/Globalization
- Light/Dark theme selection
- User authentication
- API data retrievement
- Privacy and Cookies management (RGPD)
- HTML meta management (pages title) for SEO

# Contribute

If you want to propose a feature or to report a bug, please create a new issue.
If you want to propose code source changes, please follow the steps below.

1. Installation process
   From your local computer, clone the repository.
   - `npm install` to install all dependencies

2. GitFlow
   Please follow the [GitHub Flow](https://guides.github.com/introduction/flow/):
   - Create a branch from `master`
   - Commit your code changes
   - Create a Pull Request to merge into the master `branch`

3. Conditions to complete Pull Request
   To ensure minimal quality, branch policies have been set up for pull requests to the master branch:
   - A new build must be validated before each pull request
   - A project administrator must validate the code changes

# Installation and Usage

1. Import and install MilNode (see [here](https://github.com/amilochau/milnode#readme) to know how to install MilNode)
2. Install MilNode Charts with `npm install milnode-charts`
3. In a `vue.js` page or component, import specific chart data
   ```js
import mixin from 'mixin-deep'
import light from 'milnode-charts/src/data/charts-light'
import dark from 'milnode-charts/src/data/charts-dark'

import { mapGetters } from 'vuex' // This is used to known the current theme defined in MilNode
   ```
4. Create your chart, using `highcharts-vue`:
   ```html
<template>
  <highcharts :options="chartOptions"/>
</template>
   ```
5. Define chart data from MilNode Charts resources
   ```js
export default {
  computed: {
    // Get the current theme
    ...mapGetters('theme', ['darkTheme']),

    // Use the associated Highcharts theme
    chartsTheme () {
      return this.darkTheme ? dark : light
    },

    // Create your own Highcharts chart
    chartOptions () {
      return mixin({
        chart: {
          height: 400
        },
        title: {
          text: 'Graph title'
        },
        series: [
          {
            data: [0, 1, 2, 3]
          }
        ]
      }, this.chartsTheme)
    }
  }
   ```
