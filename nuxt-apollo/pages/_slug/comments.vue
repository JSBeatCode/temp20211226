
<template>
<!-- #1 -->
    <div>
        <h1>Comments page with the slug parameter</h1>
        <p>{{$route.params.slug}}</p>
    </div>
</template>

<script>
// #1 _slug 폴더를 이용한 라우팅은, route 주소의 다변화를 가져올 수 있으며 1.comments 이 끝자리만 맞고, 2. 아래의 validation만 맞으면 화면 전개
    export default {
        validation ({params}){
            // #1 주어진 params이 정규식에 맞는지 확인해서 맞으면 true 아니면 false 및 404 에러페이지 냄
            return /^\d+$/.test(params.slug)
        }
    }
</script>

<style lang="scss" scoped>

</style> 