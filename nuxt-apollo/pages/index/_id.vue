<template>
        <!-- <div 
            v-if="!$apollo.queries.character.loading" 
            class="rounded border m-2"
        > -->
        <div>
            <img :src="character.image" />
            <div>
                <h1>{{character.status}}</h1>
                <h1>{{character.name}}</h1>
                <h1>{{character.gender}}</h1>
                <!-- <h1>{{character.origin.name}}</h1> -->
            </div>
        </div>
</template>

<script>
import gql from 'graphql-tag'
    export default {
        name: "Character",
        //   data(){
        //     console.log('jsdno0', this.$route.params.id);
        //     return {
        //         id: ((this.$route.params.id === null) || (typeof this.$route.params.id === 'undefined')) ? 1 : this.$route.params.id
        //     }
        // },
        // #5
        apollo: {
            character: {
                query: gql`
                query getCharacter($id: ID!){
                    character(id: $id){
                        id
                        name
                        status
                        species
                        gender
                        image
                        # 9
                        # origin {
                        #     name
                        # }
                    }
                }
            `,
            // #6 variables는 apollo-chracter를 실행하면 data()의 어디에 영향을 줄지 기술함
            variables(){
                    return{
                        id: this.$route.params.id
                        // id: ((this.$route.params.id === null) || (typeof this.$route.params.id === 'undefined')) ? 1 : this.$route.params.id
                    }
                }
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>