<template>
    <div class="app">
      <div class="content">
        <AppInfo :allMoviesCount="movies.length"
                 :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
        <div class="search-panel">
          <SearchPanel :updateTernHandler="updateTernHandler"/>
          <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
        </div>
        <MovieList 
        v-bind:movies="onFilterHandler(onSearchHandler(movies, term), filter)" 
        @onToggle="onToggleHandler" 
        @onRemove='onRemoveHandler'/>
        <MovieAddForm @createMovie="createMovie"/>
      </div>
    </div>
  </template>
  

  <script>
  import AppInfo from '@/components/app-info/AppInfo.vue'
  import SearchPanel from '@/components/search-panel/SearchPanel.vue'
  import AppFilter from '@/components/app-filter/AppFilter.vue'
  import MovieList from '@/components/movie-list/MovieList.vue'
  import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue'
  
  export default{
    components:{
      AppInfo,
      SearchPanel,
      AppFilter,
      MovieList,
      MovieAddForm
    },
    data() {
        return {
            movies:[
                {
                    name:'Mission Impossible',
                    viewers:800,
                    favourite: false,
                    like: true,
                    id:1,
                },
                {
                    name:'Game of Thrones',
                    viewers:650,
                    favourite: false,
                    like: false,
                    id:2,
                },
                {
                    name:'James Bond',
                    viewers:911,
                    favourite: true,
                    like: false,
                    id:3,
                },
            ],
            term: '',
            filter: 'all',
        }
    },
    methods: {
      createMovie(item){
        this.movies.push(item)
      },
      onToggleHandler({id, prop}){
        this.movies = this.movies.map(item =>{
          if(item.id == id){
            return {...item, [prop]: !item[prop]}
          }
          return item
        })
      },
      onRemoveHandler(id){
        this.movies = this.movies.filter(c => c.id !== id)
      },
      onSearchHandler(arr, term){
        if(term.length == 0){
          return arr
        }
        return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
      },
      onFilterHandler(arr, filter){
        switch(filter){
          case 'popular':
            return arr.filter(c => c.like)
          case 'mostViewers':
            return arr.filter(c => c.viewers > 500)
          default:
            return arr
        }
      },
      updateTernHandler(term){
        this.term = term
      },
      updateFilterHandler(filter){
        this.filter = filter
      }
    },
  }
 </script>
  

  <style>
  .app{
    height: 100vh;
    color: #000;
  }

  .content{
    width: 1000px;
    min-height: 700px;
    background-color: #fff;
    margin: 0 auto;
    padding: 5rem 0;
  }

  .search-panel{
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  }


  </style>