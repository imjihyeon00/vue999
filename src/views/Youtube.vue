<template>
  <div class="light">
    <Header />
    <main id="main">
      <section id="youtubeCont">
        <div class="container">
          <WrapTitle name1="youtube" name2="Reference" />
          <div class="youtube__cont">
            <form @submit.prevent="SerchMovies()">
              <div class="search">
                <label for="search" class="sr-only">검색하기</label>
                <input
                  type="search"
                  id="search"
                  placeholder="검색하기"
                  v-model="search"
                />
                <button type="submit" value="search">검색</button>
              </div>
              <div class="youtube">
                <div v-for="movie in movies" :key="movie.id.videoId">
                  <a
                    :href="
                      'https://www.youtube.com/watch?v=' + movie.id.videoId
                    "
                    target="_blank"
                  >
                    <img
                      :src="movie.snippet.thumbnails.medium.url"
                      :alt="movie.snippet.title"
                    />
                    <p className="title">{{ movie.snippet.title }}</p>
                  </a>
                </div>
              </div>
            </form>
          </div>
        </div>
      </section>
    </main>
    <ContInfo />
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import WrapTitle from '@/components/WrapTitle.vue';
import ContInfo from '@/components/ContInfo.vue';
import { ref } from '@vue/reactivity';

export default {
  components: {
    Header,
    Footer,
    WrapTitle,
    ContInfo,
  },

  setup() {
    const search = ref('');
    const movies = ref([]);
    const YOUTUBE_KEY = process.env.VUE_APP_YOUTUBE_KEY;

    const SerchMovies = () => {
      if (search.value != '') {
        fetch(
          `https://youtube.googleapis.com/youtube/v3/search?part=snippet&q=${search.value}&key=${YOUTUBE_KEY}&maxResults=30&type=video`,
        )
          .then((response) => response.json())
          .then((data) => {
            console.log(data.items);
            movies.value = data.items;
            search.value = '';
          })
          .catch((error) => console.log('error', error));
      }
    };

    return {
      search,
      movies,
      SerchMovies,
    };
  },
};
</script>

<style lang="scss">
// #youtubeCont
#youtubeCont {
  background-color: #000;
  color: #000;
}
.youtube__cont {
  .youtube {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding-bottom: 200px;

    div {
      flex: 0 0 19%;

      .title {
        font-family: 'SCoreDream';
        font-weight: 300;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        margin: 10px 0 50px;
      }
    }
  }

  .search {
    display: flex;
    justify-content: space-between;
    margin-bottom: 70px;

    input {
      flex: 0 0 79%;
      background: transparent;
      border: none;
      border-bottom: 1px solid #000;
      font-family: 'SCoreDream';
      font-weight: 300;
      padding: 15px 10px;
      outline: #000;
      color: #000;

      &::placeholder {
        color: #000;
      }
    }
    button {
      flex: 0 0 20%;
      font-family: 'SCoreDream';
      font-weight: 300;
      background-color: #000;
      border: 1px solid #000;
      color: #fff;
    }
  }
}
</style>
