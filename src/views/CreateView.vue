<script>
import axios from 'axios'
import { QuillEditor } from '@vueup/vue-quill'
import '@vueup/vue-quill/dist/vue-quill.snow.css';
export default {
  data() {
   return { 
     title: null,
     body:null,
     tags:[],
     elementVisible:false,
     status:null
   }
 },
  components: {
    QuillEditor
  },
  methods: { 
    handleTitle(e){ 
      this.title=e.target.value.substring(0, 255)
      console.log(e.target.value.substring(0, 255)) 

    },
        handleEditor(e) {
            console.log(e.value.textContent);
            this.body = e.value.textContent
        }, 
        handleTags(e){
          console.log(e.target.value) 
          this.tags = e.target.value.split(',')
          console.log(this.tags)
        },
        handleSubmit() {
          console.log("tt",this.title,this.body,this.tags)
          if(this.title){ 
         
          let param = {
            "title":this.title, 
            "description": this.body,
            "tags": this.tags,
            "votes": 0,
            "answers": 0,
            "views": 0,
            "author": "unknown"
            }

    axios
    .post(`http://localhost:3000/posts`,param)
    .then(response => (console.log(response),this.elementVisible=true,this.status="Posted"))
    .catch(error => console.log(error),this.elementVisible=true,this.status="error")  
    setTimeout(() => this.elementVisible = false, 1000)
  }
        }
    },
  
}
</script>
<template>
  <div class="create">
    <h1>Ask a public question</h1>
    <div class="flag" v-show="elementVisible">{{ status }}</div>
    <div class="field">
      <div>Title</div> 
      <sub>Be specific and imagine you’re asking a question to another person.</sub>
      <input type="text" class="textfield" @change="handleTitle($event)" />  
    </div>
    
    <div class="field">
      <div>Body</div>
      <sub>Include all the information someone would need to answer your question</sub>
      <QuillEditor theme="snow"  @blur="handleEditor($event)" toolbar="minimal" content="string" />  
       
    </div>

    <div class="field">
      <div>Tags</div> 
      <sub>Add upto 5 tags to describe what your question is about</sub>
      <input type="text" class="textfield"  placeholder="seperate by commas" @change="handleTags($event)" />  
    </div> 
    
    <div class="field">
      <button @click="handleSubmit">Submit</button>
    </div>
  </div>
</template>

<style> 
  .create { 
    width:80%;
    margin: 0 auto;
  } 
  .field{
    width:90%;
    margin:20px 10px;
  }
  .textfield { 
    width:98%;
    padding:1%;
    border: 1px solid #ddd;
  }
</style>
