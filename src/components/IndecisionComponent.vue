<template>
   <div class="container text-center">
    <div class="row">
        <div class="col"></div>
        <div class="col">
            <h1>Indecision API</h1>
        </div>
        <div class="col"></div>
    </div>
    <div class="row">
        <div class="col"></div>
        <div class="col">
            <div class="card">
                <div class="card-body">
                    <h2 class="card-title">Escribe una pregunta</h2>
                    <div v-if="isValidQuestion">
                        <h3>{{ question }}</h3>
                        <h3>{{ answer }}</h3>
                    </div>
                    <input class="form-control" type="text" v-model="question" placeholder="Hazme una pregunta">
                </div>  
                <img :src="image"  class="card-img-top" alt="">
                
            </div>
        </div>
        <div class="col"></div>
    </div>
   </div>
</template>

<script>
export default{
    data(){
        return{
            question:null,
            answer:null,
            image:null,
            isValidQuestion:false
        }
    },
    methods:{
        async getAnswer(){
            this.answer = 'Pensando...'
            const {answer,image} = await fetch('https://yesno.wtf/api').then( result => result.json() )
            this.image = image;
            this.answer = answer;
        }
    },
    watch:{
        question(value){
            if( !value.includes('?') ) return
            this.isValidQuestion = true
            this.getAnswer()
        }
    }
}
</script>