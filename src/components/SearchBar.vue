<template>
    <div class="search-box">
        <!-- type="search" 는 text 대신 시멘틱 의미 부여 -->
        <input             
            type="search" 
            @change="
             $emit('searchMovie', $event.target.value);
             inputText = $event.target.value;
             $event.target.value = '';
            "
            placeholder="검색어 입력"
        >
        <button>검색</button>
    </div>
    <p>{{  inputText }}</p>
</template>

<script>
    export default {
        name: "SearchBarComponent",
        props: {
            data: Array,
        },
        data() {
            return {
                inputText: '',
            }
        },
        watch: {
            inputText(name) {
                // 입력한 영화제목이 데이터에 있는지 확인
                const findName = this.data.filter(movie => {
                    return movie.title.includes(name);
                })
                if(findName.length == 0) {
                    alert('해당하는 자료가 없습니다.')
                }
            }
        },
        emits: ['searchMovie'],
    }
</script>

<style>
  .search-box {
    padding: 10px;
    display: flex;
    justify-content: center;
  }

  .search-box input {
    padding: 5px 10px;
  }

  .search-box button {
    margin: 0;
  }
</style>