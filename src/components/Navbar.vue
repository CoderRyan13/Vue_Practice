<template>
    <div :class="mode" id="navi"> 
        <div class="myvue">My Vue</div>
        <div v-for="(page, index) in publishedPages" :key="index">
            <div :class="page.link.class"><a class="active-a" :class="{active: activePage == index}" :href="page.link.url" :title="`This link goes to the ${page.link.text} page`"
                @click.prevent="headerLinkClick(index)">{{ page.link.text }}</a></div>
        </div>
        <button @click.prevent="checkMode" class="modeBtn">Mode</button>
    </div>
</template>

<script>
    export default {
        created() {
            this.getThemeSetting()
        },
        computed: {
            publishedPages() {
                return this.pages.filter(p => p.published);
            }
        },
        props: ['pages', 'activePage', 'headerLinkClick'],
        data() {
            return {
                mode: "header"
            }       
        },
        methods: {
            checkMode() {
        
                // if(this.mode == "header") {
                //     this.mode = "headerDark"
                // } else if(this.mode == "headerDark") {
                //     this.mode = "header"
                // }
                let mode = 'header';

                if(this.mode == 'header') {
                    mode = 'headerDark'
                }

                this.mode = mode;
                this.storeThemeSetting();
            },
            storeThemeSetting() {
                localStorage.setItem('mode', this.mode);
            },
            getThemeSetting() {
                let mode = localStorage.getItem('mode');

                if(mode) {
                    this.mode = mode;
                }
            }
        }
    }
</script>