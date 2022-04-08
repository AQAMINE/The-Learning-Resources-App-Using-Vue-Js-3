<template>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" name="title" id="title" ref="titleInput"/>
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea name="description" id="description" rows="3" ref="descInput"> </textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" name="link" id="link" ref="linkInput" />
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>


export default {
    //recive addResource method from TheResources.vue to used with our submitData() method
    inject: ['addResource'],
    methods: {
        submitData(){
            const entredTitle = this.$refs.titleInput.value;
            const entredDescription = this.$refs.descInput.value;
            const entredLink = this.$refs.linkInput.value;
            //recived method from TheResources.vue
            this.addResource(entredTitle,entredDescription,entredLink);

        }
    },
    
}
</script>

<style scoped>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
        margin: 1rem 0;
}
</style>