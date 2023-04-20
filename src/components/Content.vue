
    
 <script>   
export default {
  data() {
    return { 
      todoData: []
    }
  },
  methods: {
    async fetchData() {
      this.todoData = []
      const res = await fetch(
        `http://localhost:3000/posts`
      )
      this.todoData = await res.json()
    }
  },
  mounted() {
    this.fetchData()
  }
}
    </script>

    <template> 
    <div class="listContainer"> 
        <!-- <p>Todo id: {{ todoId }}</p> -->
  <!-- <button @click="todoId++">Fetch next todo</button> -->
  <div class="left-content"></div>
  <div class="mid-content"></div>
    <p v-if="!todoData">Loading...</p>  
    <ul v-else class="listData"> 
        <li  v-for="list in todoData" :key="list.id" class="lists">
            <div class="interactiveItems">
                <div><strong>{{ list.votes}}</strong> Votes</div>
                <div><strong>{{ list.answers}}</strong> Answers</div>
                <div><strong>{{ list.views}}</strong> Views</div>
            </div>
            <div class="listContent">
                <router-link :to="'/detail/' + list.id">
                <div class="title">{{ list.title }}</div>
                </router-link> 
                <div class="desc">{{ list.description }}</div>
                <div class="tagBox">
                    <div v-for="(tag,index) in list.tags" :key="index" class="tag">{{ tag }}</div>
                </div>
            </div > 
        </li> 
    </ul> 
    <div class="right-content"></div>
    </div>
    </template>
    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style scoped>  
    .listData{text-align: left;list-style: none;padding-left:10px;padding-right:10px;margin:0} 
    .lists{display: flex;padding:10px 5px;border-bottom:1px dashed #eee;}
    .title{color:#0074cc;font-size: 14px;margin:0;font-weight: bold;}
    .desc{font-size: 13px;}
    .tagBox{margin: 10px 0;}
    .tag{background-color: #d0e3f1;display:inline;padding: 5px;margin: 0 5px 0 0;border-radius: 4px;font-size: 12px;}
    .interactiveItems{width:150px;background-color: #fafafa;margin-right: 20px;font-size: 12px;padding: 5px;color: #555;}
    .listContainer{display: flex;width:80%;margin:0 auto}
    .mid-content{flex-grow: 8;}
    .left-content,.right-content{height: 600px;background-color: #eee;flex-grow: 1;width:300px}
    /* .listContent{} */
    </style>