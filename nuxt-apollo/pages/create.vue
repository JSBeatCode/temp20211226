<template>
    <div>
        <h2>Create Character </h2>
        <!-- #12 -->
        <form action="" @submit.prevent="createCharacter">
            <div>
                <input type="text" v-model="name" placeholder="name">
            </div> 
            <div>
                <input type="text" v-model="status" placeholder="status">
            </div> 
            <div>
                <input type="text" v-model="gender" placeholder="gender">
            </div> 
            <div>
                <input type="text" v-model="image" placeholder="image">
            </div>
            <button type="submit">Create Character</button>
        </form>
        <button @click = "onClick()" >Home</button>
    </div>
</template>

<script>
import gql from "graphql-tag"

    export default {
        name: 'CreateCharacter',
        data(){
            return {
                name: '',
                status: '',
                gender: '',
                image: '',
                // #19
                errors: []
            }
        },
        methods: {
            createCharacter(event){
                console.log('jsdno0 debug1', this.$apollo)
                this.$apollo.mutate({
                    mutation: gql`
                        mutation(
                            $name: String!
                            $status: String!
                            $gender: String
                            $image: String
                        ){
                            addCharacter(
                                name: $name,
                                status: $status,
                                gender: $gender,
                                image: $image
                            ){
                                name
                                gender
                            }
                        }
                    `,
                    variables: {
                        name: this.name,
                        status: this.status,
                        gender: this.gender,
                        image: this.image,
                    }
                }).then((data)=>{
                    event.target.reset();
                    console.log(data);
                    alert('created success!');
                })
                // #19
                .catch((e)=>{
                    console.log('errors', e.graphQLErrors);
                    this.errors = e.graphQLErrors;
                })
            },
            onClick(){
                location.href = "http://localhost:3000"
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>