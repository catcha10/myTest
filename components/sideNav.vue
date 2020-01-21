<template>
    <div class="sidenav-container"  >

        <div v-if="toggleSidebar" class="backdrop" @click="$store.dispatch('nav/toggleSidebar')"></div>

        <transition name="slide-side">
            <div v-if="toggleSidebar" class="sidenav">
                
                <div class="brand-name" >
                    <nuxt-link to="/">Logo</nuxt-link>
                </div>

                <ul class="nav-list">
                    <li class="nav-item dashboard" ><nuxt-link to="/">Dashboard</nuxt-link></li>
                    <li class="nav-item users" ><nuxt-link to="/">Users</nuxt-link></li>
                    <li class="nav-item settings" ><nuxt-link to="/">Settings</nuxt-link></li>
                    <li class="nav-item logout" ><nuxt-link to="/">Logout</nuxt-link></li>
                </ul>

            </div>
        </transition>

    </div>
</template>

<script>
    import AppLinks from '~/components/appLinks'
    export default {
        components: { AppLinks },
        computed: {
            toggleSidebar() {
                return this.$store.getters['nav/toggleSidebar']
            },
        }
    }
</script>


<style scoped>

    .sidenav-container {
        height: 100%;
        width: 100%;
    }
    .sidenav {
        height: 100%;
        width: 300px;
        background-color: #eeeeee;
        z-index: 10000;
        position: fixed;
        top: 0;
        left: 0;
        box-sizing: border-box;
        padding:20px;
    }
    .slide-side-enter-active,
    .slide-side-leave-active {
        transition: all 0.3s ease-out;
    }
    .slide-side-enter,
    .slide-side-leave-to {
        transform: translateX(-100%);
    }
    .brand-name{
        text-align:left;
        margin-bottom:15px;
        padding:10px;
    }
    .brand-name a{
        color:#fff;
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 800;
        font-size:1.2rem;
        color:#3a77b2;
        text-align:center;
        text-decoration:none;
        text-transform:uppercase;
    }

    .nav-list{
        margin:0px;
        padding:0px;
        list-style:none;
    }

    .nav-list a{
        font-family: helvetica;
        font-style: normal;
        font-weight: 300;
        font-size: 0.875rem;
        text-decoration:none;
        color:#666;
    }
    .nav-list li{
        padding:15px 10px 15px 35px;
        border-bottom:1px solid rgba(255,255,255,0.5);
        position:relative;
    }
    .nav-list li:last-child{
        border-bottom:none;
    }
    .nav-list li:before{
        font-family: 'FontAwesome';
        color:rgba(102,102,102,0.7);
        position:absolute;
        left: 10px;
        top: 15px;
    }
    li.dashboard:before{content: "\f0e4";}
    li.users:before{content: "\f0c0";}
    li.settings:before{content: "\f013";}
    li.logout:before{content: "\f08b";}
    
</style>