<template>
  <div class="app">
    <header>
      <div class="filter">
        <button @click="handleClick(0)">All</button>
        <button @click="handleClick(1)">Transport</button>
        <button @click="handleClick(2)">Caisse</button>
      </div>
    </header>    
    <FaqList :faqsFiltered="faqsFiltered"/>
  </div>
</template>

<script lang="ts">
  import { defineComponent,ref } from "vue";
  //import FaqList from './components/FaqList.vue'
  import FaqList from "@/components/FaqList.vue"
  import Faq from "@/classes/faq"
  import SoftwaresId from "@/types/Softwares"
  import axios from 'axios';
  export default defineComponent({
    name:"App",
    components:{FaqList},
    setup(){
      console.log(process.env.NODE_ENV);      
      let faqs=ref<Faq[]>([])
      let faqsFiltered=ref<Faq[]>([])
      //let faq={ id:4, question:"Pourquoi4?", answer:"Car4"}
      //faqs.value.push(faq)
      const apiUrl="http://87.98.183.225:3055"
      const nation="fr"
      const optionsFaq = {
        method: 'GET',
        url: apiUrl+"/api/faqs",
        headers: {
            'Content-Type': 'application/json',
        },
        params: {
            conditionNation: nation
        },
      };
      axios.request(optionsFaq).then(function (response) {
        response.data.data
        //console.log(response.data.data[0].id)
        for (let i = 0; i<response.data.data.length; i++) {
          //console.log(response.data.data[i])
          const faq={id:4, question:"Pourquoi4?", answer:"Car4", software:1}
          faq.id=response.data.data[i].id
          faq.question=response.data.data[i].question
          faq.answer=response.data.data[i].answer
          faq.software=response.data.data[i].productId
          //console.log(faq)
          faqs.value.push(faq)   
          faqsFiltered.value.push(faq)        
        }
        //faqsFiltered=faqs
        //console.log(faqs.value)
      }).catch(function (error) {console.error(error);})
      const software= ref<SoftwaresId>(1)
      const handleClick=(term: SoftwaresId)=>{
        software.value=term
        if (term>0){
          faqsFiltered.value=faqs.value.filter(faqs=>(faqs.software===term))
        }
        else
        {
          faqsFiltered.value=faqs.value
        }
      }
      //console.log("faq")
      //console.log(faqs.value)
      //console.log("faqsFiltered")
      //console.log(faqsFiltered.value)
      return {faqsFiltered, handleClick}
    }
  })

</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
  header .title{
    display: flex;
    justify-content: center;
  }
  header img {
    width: 60px;
    margin-right: 20px;
  }
  header h1 {
    font-size: 3em;
  }
</style>
