<template>
  <a
    class="button-social"
    :class="buttonSocialDesignObject"
    :page-url="page_url"
    :page-title="page_title"
    :button-design="button_design"
    :title-social="title_social"
    :has-icon="has_icon"
    :has-square-edges="has_square_edges"
    @click.prevent="showShareWindow"
  >
    <i class="icon-twitter" v-if="this.$props.has_icon"></i>
    <span class="title-social" v-if="this.$props.title_social">{{
      title_social
    }}</span>
  </a>
</template>

<script>
import { clickEvent } from "../helpers/events";
import { documentHref } from "../helpers/href";
import { documentTitle } from "../helpers/title";
import { openPopUpWindow } from "../helpers/popup_window";

export default {
  name: "VueGoodshareTwitter",
  props: {
    page_url: {
      type: String,
      default: documentHref
    },
    page_title: {
      type: String,
      default: documentTitle
    },
    button_design: {
      type: String,
      default: () => "flat"
    },
    title_social: String,
    has_icon: Boolean,
    has_square_edges: Boolean
  },
  data() {
    return {
      buttonSocialDesignObject: {
        "button-social__square_edges": this.$props.has_square_edges,
        twitter__design__flat: this.$props.button_design === "flat",
        twitter__design__gradient: this.$props.button_design === "gradient",
        twitter__design__outline: this.$props.button_design === "outline"
      }
    };
  },
  methods: {
    /**
     * Show share window.
     *
     * @return {object} a pop-up window
     */
    showShareWindow: function() {
      // Variables
      const width = 640;
      const height = 480;
      const share_url = `https://twitter.com/share?url=${encodeURIComponent(
        this.$props.page_url
      )}&text=${encodeURIComponent(this.$props.page_title)}`;

      // onClick event
      clickEvent(this, "twitter");

      return openPopUpWindow(share_url, width, height);
    }
  }
};
</script>

<style scoped lang="scss">
// Fontello
@font-face {
  font-family: 'Fontello';
  src: url('https://s3.amazonaws.com/assets.scenethink.com/fonts/fontello.eot?88483298');
  src: url('https://s3.amazonaws.com/assets.scenethink.com/fonts/fontello.eot?88483298#iefix') format('embedded-opentype'),
  url('https://s3.amazonaws.com/assets.scenethink.com/fonts/fontello.woff2?88483298') format('woff2'),
  url('https://s3.amazonaws.com/assets.scenethink.com/fonts/fontello.woff?88483298') format('woff'),
  url('https://s3.amazonaws.com/assets.scenethink.com/fonts/fontello.ttf?88483298') format('truetype'),
  url('https://s3.amazonaws.com/assets.scenethink.com/fonts/fontello.svg?88483298#fontello') format('svg');
  font-weight: normal;
  font-style: normal;
}

[class^="icon-"]:before,
[class*=" icon-"]:before {
  font-family: "Fontello";
  font-style: normal;
  font-weight: normal;
  speak: none;
  display: inline-block;
  text-decoration: inherit;
  width: 1em;
  margin-right: 0.2em;
  text-align: center;
  font-variant: normal;
  text-transform: none;
  line-height: 1em;
  margin-left: 0.2em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.icon-twitter:before {
  content: "\e801";
}

// Colors
$twitter_main_color: rgb(29, 161, 242);
$gradient_color: rgb(49, 181, 255);
$background_white_color: rgb(254, 254, 254);
$text_white_color: rgb(254, 254, 254);

// Reset
.button-social * {
  box-sizing: border-box;
}

// Button Social link style
.button-social {
  display: inline-flex;
  cursor: pointer;
  padding: 7px 10px;
  margin: 3px 1.5px;
  border-radius: 3px;
  -moz-border-radius: 3px;
  -webkit-border-radius: 3px;
}

// Button Social link style on hover
.button-social:hover {
  opacity: 0.9;
}

// Button Social round edges
.button-social__square_edges {
  border-radius: 0;
  -moz-border-radius: 0;
  -webkit-border-radius: 0;
}

// Button twitter style `flat`
.twitter__design__flat {
  background-color: $twitter_main_color;
  color: $text_white_color;
}

// Button twitter style `gradient`
.twitter__design__gradient {
  background-image: linear-gradient(
    to bottom,
    $twitter_main_color,
    $gradient_color
  );
  background-image: -moz-linear-gradient(
    to bottom,
    $twitter_main_color,
    $gradient_color
  );
  background-image: -o-linear-gradient(
    to bottom,
    $twitter_main_color,
    $gradient_color
  );
  background-image: -webkit-linear-gradient(
    to bottom,
    $twitter_main_color,
    $gradient_color
  );
  background-image: -ms-linear-gradient(
    to bottom,
    $twitter_main_color,
    $gradient_color
  );
  color: $text_white_color;
}

// Button twitter style `outline`
.twitter__design__outline {
  background-color: $background_white_color;
  border: 1px solid $twitter_main_color;
  color: $twitter_main_color;
}

// Title
.title-social {
  margin-left: 6px;
}
</style>
