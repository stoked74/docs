<template lang="pug">
  doc-view
    div
      section-def
        dt(slot="title") Theme
        dd(slot="desc") Vuetify offers the ability to easily change the colors of your application.
    section
      section-header Light and Dark
      section-text The default configuration is set to a light theme, but you're free to swap to a darker one by doing the following.
      section-text After setting your app theme with <code>&lt;v-app dark&gt;&lt;/v-app&gt;</code> theme, reset the material theme stylus variable:
      markup(lang="stylus")
        |$material-theme := $mterial-dark
    section
      section-header Customizing
      section-text The default theme hash looks like the example below:
      markup(lang="stylus")
        |$theme := {
        |   primary: $blue.darken-2
        |   accent: $blue.accent-2
        |   secondary: $grey.darken-3
        |   info: $blue.base
        |   warning: $amber.base
        |   error: $red.base
        |   success: $green.base
        |}
      section-text In order to change these variables, we have to create our array before the import of the Vuetify styles. You will need to setup your build process to accommodate a stylus file. If you are using one of the pre-made templates available on the <router-link to="/vuetify/quick-start">Quick Start</router-link> guide, you can skip this next section.
      h6 Setup stylus-loader with Webpack
      section-text In the command line, run:
      markup(lang="cli")
        |npm i stylus stylus-loader style-loader css-loader --save-dev
      section-text This will install the dependecies needed to import stylus files. Once installed, open your webpack config and add an additional rule:
      markup(lang="javascript")
        |{
        |   test: /\.styl$/,
        |   loader: ['style', 'css', 'stylus']
        |}
      section-text This will tell webpack how to handle a .styl file when imported. Next, we need to create the main entry point. Create a folder called <code>stylus</code> in your src directory with a file named <code>main.styl</code>. Once done, open the .styl file and add this entry.
      markup(lang="stylus")
        |// main.styl
        |@import '../../node_modules/vuetify/src/stylus/main'
      section-text Keep in mind that the relative location of node_modules may differ in your project so adjust accordingly. You have 2 options for import location, either your main <code>App.vue</code> or <code>app.js</code>.
      markup(lang="javascript")
        |// app.js
        |require('./stylus/main.styl')
      markup(lang="html")
        |// App.vue
        |&lt;style lang="stylus"&gt;
        |   @import './stylus/main'
        |&lt;/style&gt;
      section-text After you have decided on your import location, if you are requiring the Vuetify stylesheet by a &lt;link&gt; tag in your index file, remove it. Restart your build processes and re-open your project. You should see all of the styles working correctly.
      h6 Modify your theme
      section-text Now that stylus is configured, we can create a custom <code>$theme</code> hash containing the application specific styles. Keep in mind, if you want to use the built in color pack variables, i.e. <code>$grey.lighten-3</code> you will need to import the color file at the top of your <code>main.styl</code> file. For a list of colors available, navigate to the <router-link to="/style/colors">Colors</router-link> section of the documentation.
      markup(lang="stylus")
        |@import '../../node_modules/vuetify/src/stylus/settings/_colors'
        |&nbsp;
        |@import '../../node_modules/vuetify/src/stylus/main'
      section-text After you have decided on your color pallete, simply create a new hash:
      markup(lang="stylus")
        |@import '../../node_modules/vuetify/src/stylus/settings/_colors'
        |&nbsp;
        |$theme := {
        |   primary: $red.darken-2
        |   accent: $red.accent-2
        |   secondary: $grey.lighten-1
        |   info: $blue.lighten-1
        |   warning: $amber.darken-2
        |   error: $red.accent-4
        |   success: $green.lighten-2
        |}
        |&nbsp;
        |@import '../../node_modules/vuetify/src/stylus/main'
</template>

<script>
  export default {
    mounted () {
      this.$emit('view', this.meta())
    },

    preFetch () {
      return this.methods.meta()
    },

    methods: {
      meta () {
        return {
          h1: 'Theme',
          title: 'Theme | Vuetify',
          description: '',
          keywords: 'vuetify themes'
        }
      }
    }
  }
</script>
