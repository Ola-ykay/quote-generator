<template>
    <div class="quote-generator">
<div v-if="loading" class="loading">
<h2>Loading...</h2>
</div>
<div v-else class="quote-card">
    <p>'{{ quote }}'</p>
    <h3><bold>-</bold>{{ author }}</h3>
</div>
<div class="btns">
<button @click="getQuote">Generate Quote</button>
<div>
<button v-if="!showCopiedText"  @click="copyQuote">Copy Quote</button>
<button v-else>Copied</button>
</div>

</div>
</div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            loading: false,
            quote: '',
            author: '',
            showCopiedText: false,
        };
    },
    methods: {
        async getQuote() {
            this.loading = true;
            axios.get('https://api.quotable.io/random')
                .then(response => {
                    this.quote = response.data.content;
                    this.author = response.data.author;
                    setTimeout(() => {
                        this.loading = false;
                    }, 2000);
                   
                })
                .catch(error => {
                    console.log(error);
                    this.loading = false;
                });
           
        },
        copyQuote() {
            navigator.clipboard.writeText(this.quote).then(() => {
                this.showCopiedText = true;
                // window.alert('copied!');
                setTimeout(() => {
                    this.showCopiedText = false;
                }, 1000);
            }).catch(err => {
                console.log(err);
            });
        }
    },

    mounted() {
        this.getQuote();
        const link = document.createElement('link')
    link.href ="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@300&display=swap"
    link.rel = 'stylesheet'
    document.head.appendChild(link)

    }
};
</script>

<style scoped>
.quote-generator {
    width: 60%;
    height: 35vh;
    margin: 0 auto;
    padding: 20px;
    background: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}
.loading{
    font-size: 1rem;
    padding: 15px;
    
}
.quote-card{
    width: 100%;
    font-family: 'Noto Sans', sans-serif;
}
.quote-card p{
    font-size: 1rem;
    font-weight: 500;
    margin-bottom: 10px;
}
.quote-card h3{
    font-weight: 1000;
    font-size: 1rem;
}

.btns{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    gap: 30px;
}
button{
    font-size: .9rem;
    padding: 10px 20px;
    border-radius: 5px;
    background: #00416A;
    color: #fff;
    cursor: pointer;
    border: none;
    margin-top: 20px;
}
button:hover{
    background: #00416A33;
    color: #00416A;
}
button:focus{
    outline: none;
}


@media screen and (max-width: 600px){
    .quote-generator{
        width: 70%;
        height: 40vh;
    }
    .quote-card p{
        font-size: 0.8rem;
    }
    .btns{
        flex-direction: column;
        gap: 8px;

    }
    button{
        font-size: 0.8rem;
        padding: 5px 10px;
    }
}
</style>