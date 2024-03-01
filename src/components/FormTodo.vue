<template>
    <div class="form-todo form-group" style="padding: 15px">
        <p class="mb-3">
            <input placeholder="Nome" type="text" name="author" class="form-control"
                v-model="name" />
        </p>
        <p class="mb-3">
            <textarea placeholder="Comentário" name="message" class="form-control"
                v-model="message"></textarea>
        </p>
        <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
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

                this.$emit('add-todo', {
                    name: this.name,
                    message: this.message
                });
                
                this.name = '';
                this.message = '';

            },
    }
}
</script>

<style>
</style>