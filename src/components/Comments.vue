<template>
    <div class="Comments container">
            <h1>Comentários</h1>
            <hr />
            <div class="" style="padding: 15px">
                <p class="mb-3">
                    <input placeholder="nome" type="text" name="author" class="form-control"
                        v-model="name" />
                </p>
                <p class="mb-3">
                    <textarea placeholder="Comentário" name="message" class="form-control"
                        v-model="message"></textarea>
                </p>
                <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
            </div>

            <div class="list-group">
                <p v-if="comments.length <= 0">Sem comentários ... </p>
                <p v-else>Veja abaixo os comentários:</p>
                <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
                    <span class="comment__author">Author: <strong>{{comment.name}}</strong></span>
                    <p>{{comment.message}}</p>
                    <div>
                        <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
                    </div>
                </div>

            </div>

            <hr />
        </div>
</template>

<script>
export default {
    name: "Comments",
    data() {
            return {
                comments: [
                    {
                        name: '',
                        message: 'mensagem de teste'
                    },
                    {
                        name: 'Sena',
                        message: 'Campeão'
                    }
                ],
                name: '',
                message: ''
            }
        },
        methods: {
            addComment() {

                if (this.message.trim() == '') {
                    alert('Preencha a mensagem!')
                    return;
                }
                
                this.comments.push({
                    name: this.name,
                    message: this.message
                });

                this.name = '';
                this.message = '';

            },
            removeComment(index) {
                this.comments.splice(index, 1);
            }
        },
        computed: {
            allComments() {
                return this.comments.map(comment => ({
                    ...comment,
                    name: comment.name.trim() === '' ? 'Anônimo' : comment.name
                }))
            }
        },
        watch: {
            comments(val) {
                console.log('val', val)
            }
        }
    }
</script>

<style>
</style>