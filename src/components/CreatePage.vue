<template>
    <div class="container">
        <form action="">
            <div>
                <label for="">
                    Page Title
                </label>
                <input
                    type="text"
                    class="form-control"
                    v-model="pageTitle"
                />
            </div>
            <div>
                <label>
                    Content
                </label>
                <textarea
                    type="text"
                    class="form-control"
                    rows="5"
                    v-model="content"
                ></textarea>
            </div>
            <div>
                <label for="">
                    Link Text
                </label>
                <input
                    type="text"
                    class="form-control"
                    v-model="linkText"
                />
            </div>
            <div>
                <label for="">
                    Link URL
                </label>
                <input
                    type="text"
                    class="form-control"
                    v-model="linkUrl"
                />
            </div>
            <div>
                <div>
                    <input type="checkbox" v-model="published">
                    <label>Published</label>
                </div>
            </div>
            <div>
                <button
                    class="modeBtn"
                    :disabled="isFormInvalid"
                    @click.prevent="submitForm"
                >Create Page</button>
            </div>
        </form>
    </div>
</template>
<script>
    export default {
        props: ['pageCreated'],
        computed: {
            isFormInvalid() {
                return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl;
            }
        },
        data() {
            return {
                pageTitle: '',
                content: '',
                linkText: '',
                linkUrl: '',
                published: true
            }
        },
        methods: {
            submitForm() {
                if(!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
                    alert('Please fill out the form.');
                    return;
                }

                this.pageCreated({
                    pageTitle: this.pageTitle,
                    content: this.content,
                    link: {
                        text: this.linkText,
                        url: this.linkUrl,
                        class: 'about'
                    },
                    published: this.published
                })

                this.pageTitle = '';
                this.content = '';
                this.linkText = '';
                this.linkUrl = '';
                this.published = true;
            }
        }
    }
</script>