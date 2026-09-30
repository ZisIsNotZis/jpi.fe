<template>
    <button v-for="i in names" @click="setname(i)">{{ i }}</button>
    <Trees v-model="dat" @save="save" @del="del" />
    <div>
        <button @click="setpage(-1)">&lt;</button>
        {{named}} / {{ page }} / {{ pages }}
        <button @click="setpage(1)">&gt;</button>
    </div>
</template>

<script>
import Trees from './components/Trees.vue';
import axios from 'axios';

export default {
    components: {
        Trees
    },
    data() {
        return {
            names: [],
            named: "select entity",
            dat: [{a:3,b:4},{a:4,b:5,c:{c1:5,c2:6}}],
            page: '?',
            pages: '?'
        };
    },
    created() {
            axios.get(`//127.0.0.1:8080/api`).then(x => {
                this.names = x.data
            })
    },
    methods: {
        setname(i) {
            this.named = i
            this.page = 1
            this.pages = 1
            axios.get(`//127.0.0.1:8080/api/${i}`).then(x => {
                this.dat = x.data.content
                this.pages = x.data.page.totalPages
            })
        },
        setpage(i) {
            axios.get(`//127.0.0.1:8080/api/${this.named}?page=${this.page - 1}`).then(x => {
                this.dat = x.data.content
                this.pages = x.data.page.totalPages
            })
        },
        save(i) {
            axios.post(`//127.0.0.1:8080/api/${this.named}`, this.dat[i]).then(x=> this.dat[i] = x.data);
        },
        del(i) {
            axios.delete(`//127.0.0.1:8080/api/${this.named}/${this.dat[i].id}`)
        },
    }
};
</script>