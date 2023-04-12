<template>
    <div class="faq-list">
        <ul>
            <li v-for="faq in faqsFiltered" :key="faq.id">
                <h2>{{ faq.question }}</h2>
                <div class="answer">
                    <p>{{ faq.answer }}</p>
                </div>              
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
    import { defineComponent, PropType } from 'vue';
    //import Faq from '../classes/faq'
    import Faq from '@/classes/faq'
    export default defineComponent({
        props: {
            faqsFiltered:{
                required:true,
                type: Array as PropType<Faq[]>
            }
        }
    })
</script>

<style scoped>
  .faq-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .faq-list ul {
    padding: 0
  }
  .faq-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .faq-list h2 {
    margin: 0 0 10px;
  }
  .answer {
    display: flex;
  }
  .answer img {
    width: 30px;
  }
  .answer p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move {
    transition: all 1s;
  }
</style>