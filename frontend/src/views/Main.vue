<template>
  <section id="one" class="wrapper">
    <div class="inner split">
      <section>
        <h1 id="currentList">현재 응급 상황 목록</h1>
        <hr>
        <div class="cur_emer_contents">
          <div v-for="(current_emergency, id) in current_emergencies" :key="current_emergency.id">
            <router-link :to="{ name: 'detail', params: {id: current_emergency.id }}" class="contents">{{ subDate(current_emergency.time) }}</router-link>
            <hr v-if="id != current_emergency.length">
          </div>
        </div>
      </section>
      <section>
        <ul class="googleMap">
          googlemap here
        </ul>
      </section>
    </div>
  </section>

</template>

<script>
    import axios from 'axios';
    export default {
        data (){
          return{
              current_emergencies : []
          }
        },
        methods: {
            subDate(date){
                var subDate = date.substring(0,22);
                var pardsedDate = subDate.split('T');
                return pardsedDate[0] + " " + pardsedDate[1];
            },
        },
        async beforeCreate() {
            const current_result = await axios.get("/api/current/c_emer");
            this.current_emergencies = current_result.data;
        },
    }
</script>

<style>

  #currentList{
    text-align: center;
  }

  html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
  }

  ol, ul {
    list-style: none;
  }

</style>
