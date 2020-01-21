<template>
    <div>
        <ul class="topNav" >
            <li><nuxt-link to="/" title="Profile"  ><font-awesome-icon icon="user-circle" size="lg" /></nuxt-link></li>
            <li><nuxt-link to="/" title="Notifications" ><font-awesome-icon icon="bell" size="lg" /><span class="badge" >2</span></nuxt-link></li>
            <li><nuxt-link to="/" title="Activity Log" ><font-awesome-icon icon="list" size="lg" /></nuxt-link></li>
        </ul>
    </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faUserCircle, faBell, faList } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faUserCircle, faBell, faList)

export default {
    components: { 
        FontAwesomeIcon, 
    },
}
</script>

<style scoped  >
    .nav-list {
        list-style: none;
        padding: 0;
        margin: 0;
        margin-right:15px;
    }
    .nav-item {
        margin: 0 10px;
    }
    .nav-item a {
        text-decoration: none;
        color: #fefefe;
        font-family: 'Roboto';
        font-style: normal;
        font-weight: 400;
        font-size:0.875rem;
    }
    .nav-item a:hover,
    .nav-item a:active{
        color: #b4b4b4;
    }
    .app-links .brand-name{
        display:none;
    }
    .sidenav .topNav{display:none;}
    
    .topNav{
        margin:0px 20px 0 0;
        padding:0px;
        list-style:none;
    }
    .topNav li{
        float:right;
        padding:0 10px;
    }
    .topNav li a{
        font-size:1.1rem;
        color:rgba(255,255,255,0.8);
        position:relative;
    }
    .badge{
        display: inline-block;
        width: 15px;
        height: 15px;
        border-radius: 50%;
        background-color: #e61f2d;
        color: #fff;
        font-size: 10px;
        text-align: center;
        line-height: 15px;
        font-family: helvetica;
        position:absolute;
        top: -8px;
        right: -6px;
    }
    @media (max-width: 767px) {
        .sidenav .topNav{display:block;}
        .nav-list {
            display: block;
        }
        .nav-item{
            margin-top: 16px;
            margin-bottom: 16px;
        }
        .sidenav .topNav{display:block;}
    }
    
</style>