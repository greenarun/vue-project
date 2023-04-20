
    
 <script>   
 import axios from 'axios'
export default {
  data() {
    return { 
      todoData: [],
      total:40, 
      pages:0,
    }
  },
  methods: {
    async fetchData() { 
      axios
    .get(`http://localhost:3000/posts?_page=${this.pages}&_limit=15`)
    .then(response => (this.todoData = response.data))
    .catch(error => console.log(error))   
    },
    handlePagination(item){
      this.pages=item
      this.fetchData()

    }
  },
  mounted() {
    this.fetchData()
    
  }
}
    </script>

    <template> 
    <div>
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
    <div class="pagination">
      <ul>
        <button v-for="item in Math.ceil(total/15)" @click="handlePagination(item)">{{ item }}</button>
      </ul>
    </div>
  </div>
    </template>
    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style scoped>  
    .listData{text-align: left;list-style: none;padding-left:10px;padding-right:10px;margin:0;overflow-y: auto;height: 600px;width:100%} 
    .lists{display: flex;padding:10px 5px;border-bottom:1px dashed #eee;}
    .title{color:#0074cc;font-size: 14px;margin:0;font-weight: bold;}
    .desc{font-size: 13px;}
    .tagBox{margin: 10px 0;}
    .tag{background-color: #d0e3f1;display:inline;padding: 5px;margin: 0 5px 0 0;border-radius: 4px;font-size: 12px;}
    .interactiveItems{width:20%;background-color: #fafafa;margin-right: 20px;font-size: 12px;padding: 5px;color: #555;}
    .listContainer{display: flex;width:80%;margin:0 auto}
    .listContent{width:80%}
    .mid-content{flex-grow: 8;}
    .left-content,.right-content{height: 600px;background-color: #eee;flex-grow: 1;width:300px}
    .pagination{width:80%;margin: 0 auto;}
    .pagination ul{padding:0;}
    .pagination button{margin:0 5px;cursor: pointer;}
    /* .listContent{} */
    </style>