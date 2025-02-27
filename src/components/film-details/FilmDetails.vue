<template>
  <div class='film-details'>
    <div class="film-details_layer layer">
      <div class="layer_image"/>
    </div>
    <div class="film-details_film film" v-if="!!film">
      <div class="film_poster">
        <img :src="film.posterUrl" @error="$replaceImg404"/>
      </div>
      <div class="film_info info">
        <div class="info_title-block title-block">
        <span class="title-block_title">
          {{film.title}}
        </span>
          <div class="title-block_rating rating">
            <span class="rating_value">{{film.rating}}</span>
          </div>
        </div>
        <div class="info_genre">
          <span>{{film.genres?.join(', ')}}</span>
        </div>
        <div class="info_stats stats">
          <div class="stats_year year">
            <span class="year_value">{{ film.year }}</span>
            <span class="year_units">{{$translate('YEAR')}}</span>
          </div>
          <div class="stats_duration duration">
            <span class="duration_value">{{film.runtime}}</span>
            <span class="duration_units">{{$translate('MIN')}}</span>
          </div>
        </div>
        <div class="info_plot">
          <p>{{film.plot}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex';
import * as actions from '../../store/actions';
import { DEFAULT_SELECTED_FILM_ID } from '../../constants/common';

export default {
  name: 'FilmDetails',
  beforeMount() {
    if (!this.film || (this.$route?.params?.id && this.film.id?.toString() !== this.$route?.params.id)) {
      console.log('> ', this.film);
      const id = this.$route?.params.id || DEFAULT_SELECTED_FILM_ID;
      this.selectedChange(id);
    }
  },
  computed: mapState({
    film: state => state.film
  }),
  methods: mapActions({
    selectedChange: actions.SELECTED_CHANGE,
  }),
};
</script>

<style scoped lang="less">
@import "../../assets/css/variables.less";

.film-details {
  display: flex;
  position: relative;
  overflow: hidden;
  padding: 80px 60px 50px 60px;
  .fontMixin(24px);
  color: @primaryText;
}

.film-details_layer {
  .layerMixin("../../assets/img/cinema.jpg", 5px, 0.4);
}

.film_poster {
  height: 400px;
  width: 300px;

  img {
    height: 100%;
  }
}

.film-details_film {
  display: flex;
}

.film_info {
  padding: 12px 0 12px 60px;
}

.title-block {
  display: flex;
  align-items: center;
}

.title-block_title {
  font-size: 30px;
}

.title-block_rating {
  .boxMixin(40px);
  font-size: 18px;
  border: 1px solid @primaryTextOpacity;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 20px;
}

.rating_value {
  color: @positiveText;
}

.info_genre {
  font-size: 16px;
  margin-top: 10px;
}

.info_stats {
  margin-top: 30px;
  display: flex;
}

.stats_year {
  margin-right: 20px;
}

.year_value {
  margin-right: 5px;
}

.year_units {
  color: @activeText;
}

.duration_value {
  margin-right: 5px;
}

.duration_units {
  color: @activeText;
}

.info_plot {
  margin-top: 20px;
  font-size: 18px;
  line-height: 1.4;
}

@media only screen and (max-width: 600px) {
  .film-details {
    padding: 80px 10% 50px 10%;
  }

  .film {
    flex-direction: column;
    align-items: center;
  }

  .info {
    padding: 20px 0 0 0;
  }

  .film_poster,
  .info_plot,
  .info_stats,
  .title-block,
  .info_genre {
    display: flex;
    justify-content: center;
  }

  .info_plot p {
    text-align: center;
  }
}
</style>
