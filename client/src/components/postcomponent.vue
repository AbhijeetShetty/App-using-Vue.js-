<template>
    <div class="container"> 
      <h1> Latest Post</h1>
      <hr>
      <p class="error" v-if="error">{{error}}</p>
      <div class="posts-container">
        <div class="post" 
        v-for="(post,index) in posts"   
        v-bind:item="post"
        v-bind:index="index"
        v-bind:key="post.id"        
        >
        
        {{`${post.createdAt.getDate()}/${post.createdAt.getMonth()}`}}
        <p class="text">{{post.text}}</p>

      </div>
    </div>
    </div>
</template>

<script>
import postsevice from '../postservice';
export default {
  name: 'postcomponent',
  data(){
    return {
      posts: [],
      error: '',
      text: ''
    }
  },
  async created(){
    try{
      this.posts = await postsevice.getPosts();

    }catch(err){
      this.error = err.message;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div.container{
  max-width: 800px;
  margin:0 auto;
}
p.error {
border: 1px solid #ff5b5f;
background-color: aliceblue;
padding: 10px;
margin-bottom: 20px; 
}

div.post{
  position: relative;
  border: 1px solid #49a037;
background-color: aliceblue;
padding: 10px 10px 30px 10px;
margin-bottom: 20px;

}

div.created-at{
  position: absolute;
  top: 0;
  left: 0;
  
background-color: rgb(20, 104, 5);
padding: 5px 15px 5px 15px;
color: white;
font-size: 13px;


}


p.text
{
  font-size: 22px;
  font-weight: 700;
  margin-bottom: 0;
}
</style>
