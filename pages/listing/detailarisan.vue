<template>
    <div class="arisan-container">
        <div class="row justify-content-center px-md-5">
            <h1 class="text-center">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
            </h1>
        </div>
        <div class="row justify-content-center px-md-5 margin-top-40">
            <span class="arisan-text text-justify">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
            </span>
        </div>
        <div class="row justify-content-center px-md-5 margin-top-40">
            <button @click.prevent="completeProfile" class="btn btn-primary" type="submit">
                <i class="fas fa-smile" /> Ikut
            </button>
        </div>
        <div class="row justify-content-center px-md-5 margin-top-40">
            <a @click.prevent="arisanList" href="#">Lihat lainnya</a>
        </div>
    </div>
</template>
<script>
export default {
    methods: {
        arisanList(){
            this.$router.push('/listing/arisan')
        }
    }
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Trocchi&display=swap');
h1 {
    color: #7c795d;
    font-family: 'Trocchi', serif;
    font-size: 30px;
    font-weight: normal;
    line-height: 48px;
    margin: 0;
}
.arisan-container {
    background-color: #f3f3f3;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    -webkit-transition: all 0.3s cubic-bezier(.25,.8,.25,1);
    transition: all 0.3s cubic-bezier(.25,.8,.25,1);
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    margin-top: 50px;
    padding-top: 50px;
    padding-bottom: 50px;
    margin-bottom: 40px;
}
.arisan-container a{
    display: block;
    padding-top:10px;
    color:lightseagreen;
}
.margin-top-40 {
    margin-top: 40px;
}
.display-block {
    display: block;
}
.tanggal-group {
    display: inline-block;
}
</style>