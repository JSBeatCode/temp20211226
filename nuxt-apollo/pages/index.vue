<template>
  <!-- <Tutorial/> -->
  <div class="container">
    <h1>nuxt apollo test</h1>
    <nuxt-link to ="create">Create Character</nuxt-link>
    <!-- <h3 class="text-2xl"> -->
      <!-- #5 #7 apollo의 character 실행해서 보여지는 결과물 -->
      <!-- {{ character.id }} - {{ character.name }} -->
    <!-- </h3> -->
    <!-- #5 클릭하면 data()내의 characterId를 변경 -> 변경된 characterId는 apollo-character-variables의 id에 영향 -> character로 보여지는 위의 결과물도 영향 -->
    <!-- <button @click="characterId = characterId + 1" class="bg-grey 700 p-4 border text-white">Get Next Character</button> -->
    <div class="flex">
      <ul class="w-64 -px-2 text-gray-700">
        <!-- #7 #8 apollo characters에서 실행해서 보여지는 결과물  -->
          <li v-for="character in characters" :key="character.id">
            <nuxt-link :to="character.id" class="hover:font-bold hover:text-gray-900 leading-loose">
              {{ character.name }} - {{ character.id }}
            </nuxt-link>
          </li> 
      </ul>
      <!-- #8 -->
      <div class="flex-grow bg-white min-h-full">
        <!-- <nuxt-child :key="$route.params.id"> -->
        <nuxt-child>
        </nuxt-child>
      </div>
    </div>
    <button @click = "testMethod()" >test</button>
  </div>
</template>

<script>
import gql from 'graphql-tag';
export default {
  // #6
  // data(){
  //   return {
  //     characterId: 1
  //   }
  // },
  // #17
  methods: {
    testMethod(){
      console.log('jsdno0 debug1', this.$apollo);
    }
  },
  async asyncData({app, redirect}){
    const result = await app.apolloProvider.defaultClient.query({
      query: gql`
        query getCharacters{
          characters {
              id
              name
          }
        }
      `,
    });

    

    redirect('/'+result.data.characters[0].id);

    return result.data
  },
  // #10
  // fetch({redirect, route}){
    // if(!route.params.id){
    //   redirect('/1');
    // }
  // },
  // #4
  // apollo:{
  //   characters: { 
  //     query: gql`
  //       query getCharacters{
  //         characters {
  //             id
  //             name
  //         }
  //       }
  //     `,
  //     // # 16
  //     // result({data, loading, networkStatus}){
  //     //   this.$router.push(data.characters[0].id)
  //     // }
  //   },
    // // #5
    // character: {
    //     query: gql`
    //     query getCharacter($id: ID!){
    //       character(id: $id){
    //         id
    //         name
    //       }
    //     }
    //   `,
    //   // #6 variables는 apollo-chracter를 실행하면 data()의 어디에 영향을 줄지 기술함
    //   variables(){
    //     return{
    //       id: this.characterId
    //     }
    //   }
    // }
  // }
}
</script>
