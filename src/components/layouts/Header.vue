<template>
  <nav
    v-if="$route.name !== 'api.index_page'"
    id="header_navigation"
    class="navigation"
  >
    <div id="header_logo" class="logo">
      <router-link :to="'/'" exact>
        <img
          id="header_logo-txt"
          alt="t1nkl - Web Developer - Logo"
          class="logo-txt"
          height="199"
          src="../../assets/logo.png"
          width="380"
        />
        <div class="logo-bg-holder">
          <div id="header_oval-big" class="logo-bg oval-big"></div>
          <div id="header_oval-small" class="logo-bg oval-small"></div>
          <div id="header_circle" class="logo-bg circle"></div>
        </div>
      </router-link>
    </div>

    <div id="header_main-navigation" class="main-navigation">
      <ul>
        <li>
          <router-link :to="'/skills'" exact> skills<span>.</span></router-link>
        </li>
        <li>
          <router-link :to="'/works'" exact> works<span>.</span></router-link>
        </li>
        <li>
          <router-link :to="'/life'" exact> life<span>.</span></router-link>
        </li>
        <li>
          <router-link :to="'/contact'" exact> contact<span>.</span></router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { Back, Expo, gsap, TimelineMax } from 'gsap'
import { CSSPlugin } from 'gsap/CSSPlugin'

gsap.registerPlugin(CSSPlugin)

export default {
  name: 'Header',
  data: () => ({
    timeline: new TimelineMax(),
  }),
  methods: {
    animateNavigation () {
      document.getElementById('#header_oval-big') &&
      document.getElementById('#header_oval-big').classList.remove('rotating-fast')
      document.getElementById('#header_oval-small') &&
      document.getElementById('#header_oval-small').classList.remove('rotating-slow')

      this.timeline.set('#header_circle', {
        scale: 0,
        z: 0.01,
      })

      this.timeline.set('#header_oval-small', {
        autoAlpha: 0,
        scale: 0,
        z: 0.01,
      })

      this.timeline.set('#header_oval-big', {
        autoAlpha: 0,
        scale: 0,
        z: 0.01,
      })

      this.timeline.set('#header_logo-txt', {
        autoAlpha: 0,
        z: 0.01,
      })

      this.timeline.set('#header_main-navigation', {
        autoAlpha: 0,
        z: 0.01,
      })

      this.timeline.fromTo(
        '#header_circle',
        3,
        {
          scale: 0,
          transformOrigin: '50% 50%',
        },
        {
          force3D: true,
          scale: 1,
          transformOrigin: '50% 50%',
          ease: Back.easeOut.config(2.25),
        },
      )

      this.timeline.fromTo(
        '#header_oval-small',
        2.5,
        {
          autoAlpha: 0,
          scale: 0,
          transformOrigin: '50% 50%',
        },
        {
          force3D: true,
          autoAlpha: 0.45,
          scale: 1,
          transformOrigin: '50% 50%',
          ease: Back.easeOut.config(2.25),
        },
        '-=2.25',
      )

      this.timeline.fromTo(
        '#header_oval-big',
        2.5,
        {
          autoAlpha: 0,
          scale: 0,
          transformOrigin: '50% 50%',
        },
        {
          force3D: true,
          autoAlpha: 0.25,
          scale: 1,
          transformOrigin: '50% 50%',
          ease: Back.easeOut.config(2.25),
        },
        '-=2.25',
      )

      this.timeline.fromTo(
        '#header_logo-txt',
        2.5,
        { autoAlpha: 0, x: -80 },
        {
          autoAlpha: 1,
          x: 0,
          ease: Expo.easeOut,
        },
        '-=2.65',
      )

      this.timeline.fromTo(
        '#header_main-navigation',
        2.5,
        { autoAlpha: 0, x: -80 },
        {
          autoAlpha: 1,
          x: 0,
          ease: Expo.easeOut,
        },
        '-=2.5',
      )

      setTimeout(function () {
        document.getElementById('#header_oval-big') &&
        document.getElementById('#header_oval-big').classList.add('rotating-fast')
        document.getElementById('#header_oval-small') &&
        document.getElementById('#header_oval-small').classList.add('rotating-slow')
      }, 2000)
    },
  },
  watch: {
    $route (to, from) {
      if (from.name === 'api.index_page') {
        this.$nextTick().then(() => {
          this.animateNavigation()
        })
      }
    },
  },
  mounted () {
    this.animateNavigation()
  },
}
</script>

<style lang="scss">
// mixins - media query
@mixin maxquery($width, $ratio: false) {
  @if $ratio {
    @media only screen and (max-width: $width) and (min--moz-device-pixel-ratio: $ratio),
    only screen and (max-width: $width) and (-webkit-min-device-pixel-ratio: $ratio),
    only screen and (max-width: $width) and (min-device-pixel-ratio: $ratio) {
      @content;
    }
  } @else {
    @media only screen and (max-width: $width) {
      @content;
    }
  }
}

nav {
  &.navigation {
    position: relative;
    display: block;
    width: 98%;
    width: calc(100% - 32px);
    height: auto;
    padding: 84px 16px;
    // logo
    .logo {
      position: relative;
      display: block;
      max-width: 120px;
      height: auto;
      float: left;
      @include maxquery(640px) {
        width: 260px;
        height: auto;
      }

      .logo-txt {
        position: relative;
        z-index: 4;
        width: 50px;
        height: auto;
        margin: 3px;
        opacity: 0;
        visibility: hidden;
      }

      .logo-bg-holder {
        position: absolute;
        display: block;
        width: 256px;
        height: auto;
        margin-top: -25px;
        left: -80px;
      }

      .logo-bg {
        position: absolute;
        display: block;
        width: 100%;
        height: 100%;
        -moz-border-radius: 50%;
        -webkit-border-radius: 50%;
        border-radius: 50%;
        top: 50%;
        left: 50%;
        box-shadow: 0 0 7px rgba(0, 0, 0, 0.015), 0 0 7px rgba(0, 0, 0, 0.05);

        &.oval-big {
          width: 76px;
          height: 82px;
          background: #a5d6a7;
          margin-top: -41px;
          margin-left: -38px;
          z-index: 1;
          opacity: 0;
          visibility: hidden;
        }

        &.oval-small {
          width: 68px;
          height: 60px;
          background: #a5d6a7;
          margin-top: -30px;
          margin-left: -34px;
          z-index: 2;
          opacity: 0;
          visibility: hidden;
        }

        &.circle {
          width: 48px;
          height: 48px;
          background: #a5d6a7;
          transform: translate(-50%, -50%);
          z-index: 3;
        }
      }
    }

    // navigation main
    .main-navigation {
      position: relative;
      z-index: 5;
      opacity: 0;
      visibility: hidden;

      ul {
        position: relative;
        display: block;
        overflow: hidden;
        width: 100%;
        max-width: 260px;
        list-style-type: none;
        padding: 0;
        margin: 0;
        right: -10px;
        float: right;
        @include maxquery(640px) {
          max-width: 124px;
          top: -24px;
        }

        li {
          position: relative;
          display: block;
          float: left;
          padding: 8px;
          @include maxquery(640px) {
            width: calc(100% - 16px);
            display: block;
            text-align: right;
            padding-top: 0;
            padding-bottom: 0;
          }

          a {
            font-family: "Cardo", serif;
            text-decoration: none;
            color: #363636;
          }
        }
      }
    }
  }
}

@-webkit-keyframes rotating /* Safari and Chrome */
{
  from {
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}

@keyframes rotating {
  from {
    -ms-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -ms-transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}

.rotating-fast {
  -webkit-animation: rotating 12s linear infinite;
  -moz-animation: rotating 12s linear infinite;
  -ms-animation: rotating 12s linear infinite;
  -o-animation: rotating 12s linear infinite;
  animation: rotating 12s linear infinite;
}

@-webkit-keyframes rotating-inverse /* Safari and Chrome */
{
  from {
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -webkit-transform: rotate(-360deg);
    -o-transform: rotate(-360deg);
    transform: rotate(-360deg);
  }
}

@keyframes rotating-inverse {
  from {
    -ms-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -ms-transform: rotate(-360deg);
    -moz-transform: rotate(-360deg);
    -webkit-transform: rotate(-360deg);
    -o-transform: rotate(-360deg);
    transform: rotate(-360deg);
  }
}

.rotating-slow {
  -webkit-animation: rotating-inverse 16s linear infinite;
  -moz-animation: rotating-inverse 16s linear infinite;
  -ms-animation: rotating-inverse 16s linear infinite;
  -o-animation: rotating-inverse 16s linear infinite;
  animation: rotating-inverse 16s linear infinite;
}
</style>
