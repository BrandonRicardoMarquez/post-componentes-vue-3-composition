<!-- <script>
export defau
  components: { BlogPost },lt{
  data() {
    return {
      counter: 0
    }
  },
  methods: {
    increment(){
      this.counter ++
    }
  }
}
</script> -->


<script setup>
  // import ButtonCounter from './components/ButtonCounter.vue'
  import { computed, onMounted, ref } from "vue"
  import PagPost from './components/PagPost.vue';
  import BlogPost from './components/BlogPost.vue';
  import Loadingpage from './components/Loadingpage.vue';

  const posts = ref([ ""
    // {title: 'Post 1', id: 1, body: 'descripcion 1'},
    // {title: 'Post 2', id: 2, body: 'descripcion 2'},
    // {title: 'Post 3', id: 3, body: 'descripcion 3'},
    // {title: 'Post 4', id: 4, body: 'descripcion 4'},
  ])
  const postppage = 3
  const inicio = ref(0)
  const fin = ref(postppage)
  const loading = ref(true);
  
  const favorito = ref('')
  const cambiarFavorito = (title) => {
    favorito.value  = title
  };

  const next = () => {
    inicio.value = inicio.value + postppage;
    fin.value = fin.value + postppage;
  }

  const preview = () => {
    inicio.value = inicio.value - postppage;
    fin.value = fin.value - postppage;
  }

  // onMounted(async() => {
  //   loading.value = true;
  //   try{
  //     const res = await fetch("https://jsonplaceholder.typicode.com/posts")
  //     posts.value = await res.json()
  //   }catch (error) {
  //     console.log(error)
  //   } finally {
  //     setTimeout(() =>{
  //       loading.value = false
  //     },1000)
  //   }
  // })
      // fetch('https://jsonplaceholder.typicode.com/posts')
    //   .then(res => res.json())
    //   .then((data) => {
    //     posts.value = data;  
    // })
    // .catch((e) => console.log(e))
    // // .finally(() => (loading.value = false))
    // .finally(() => {
    //   setTimeout(() =>{
    //     loading.value = false
    //   },1000)
    // })

    const fetchData = async () => {
      try{
        const res = await fetch("https://jsonplaceholder.typicode.com/posts")
        posts.value = await res.json()
      }catch (error) {
        console.log(error)
      } finally {
        setTimeout(() =>{
          loading.value = false
        },1000)
      }
    }

    fetchData();

const maxLength = computed(() => posts.value.length)
</script>

<template >
  <Loadingpage  v-if="loading"/>
  <div class="container mb-4" v-else>
    <h1>APP</h1>
    <h2>Mis Post Favorito: {{ favorito }}</h2>

    <!-- <button @click="next" class="btn btn-primary">Next Preview</button>
    <button @click="preview" class="btn btn-primary">prev Preview</button> -->
    <PagPost 
        class="mb-2" 
        @next="next" 
        @prev="preview" 
        :inicio="inicio" 
        :fin="fin"
        :maxLength = "maxLength"
    />
        

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
        :key="post.id" 
        :title="post.title" 
        :id="post.id" 
        :body="post.body" 
        @cambiarFavoritoNombre="cambiarFavorito"
        class="mb-2"
    />
    <!-- <BlogPost 
      title="Post 2" 
      :id="post.id" 
      body="descripcion 2" 
      
    />
    <BlogPost 
      title="Post 3" 
      :id="3" 
      body="descripcion 3" 
      
    />
    <BlogPost 
      title="Post 4" 
      :id="4" 
      body="descripcion 4" 
      
    /> -->
  </div>
</template>
