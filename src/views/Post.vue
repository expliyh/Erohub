<template>
  <div>
    <div class="masonry" v-html="meta.text"></div>
  </div>
</template>

<script>
import axios from "axios";
import NProgress from 'nprogress'
import 'nprogress/nprogress.css'
import Icon from "@/components/Icon";

export default {
  components: {Icon},
  data() {
    return {
      meta: undefined,
    }
  }
  ,
  created() {
    NProgress.start()
    NProgress.set(0.4)
    axios.get('https://cdn.jsdelivr.net/gh/AsahiIndustry/erohub-backend@latest/dist/post/' + this.$route.params.post + '.json')
        .then(response => (this.meta = response.data.data)(document.title = response.data.data.title + ' - Erohub'))
        .catch(error => {
          console.log(error)
        })
    NProgress.done()
  }
}

</script>

<style scoped>

.masonry {
  margin: 20px auto;
  columns: 4;
  column-gap: 30px;
}

.masonry :deep(img) {
  margin-bottom: 30px;
}

@media screen and (min-width: 1024px) and (max-width: 1440px) {
  .masonry {
    columns: 3;
    column-gap: 20px;
  }
}

@media screen and (min-width: 768px) and (max-width: 1024px) {
  .masonry {
    columns: 3;
    column-gap: 20px;
  }
}

@media screen and (max-width: 768px) {
  .masonry {
    columns: 1;
  }

  .masonry :deep(img) {
    margin-bottom: 20px;
  }

}
</style>
