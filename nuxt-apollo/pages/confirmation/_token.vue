<template>
    <div>
        <h1 v-if="confirmEmail"> You have confirmed email address </h1>
    </div>
</template>

<script>
import gql from "graphql-tag";

    export default {
        name: "confirmationEmail",
        async asyncData({params, app}){
            const {token} = params;
            // #26
            const isValid = await app.apolloProvider.defaultClient.mutate({
                mutation: gql`
                    mutation($token: String!){ 
                        confirmEmail(token: $token)
                    }
                `,
                variables: {
                    token
                }
            })
            return isValid.data;
        }
    }
</script>

<style lang="scss" scoped>

</style>