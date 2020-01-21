<template>
    <ul class="editNav" >
        <li><nuxt-link to="/" title="Delete" ><font-awesome-icon icon="trash-alt" size="lg" /></nuxt-link></li>
        <li><nuxt-link to="/" title="Edit"  ><font-awesome-icon icon="edit" size="lg" /></nuxt-link></li>
    </ul>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faEdit, faTrashAlt } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faEdit , faTrashAlt)

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
    .sidenav .editNav{
        display:none;
    }
    .editNav{
        margin:0px;
        padding:0px;
        list-style:none;
        display:inline-block;
    }
    .editNav li{
        float:right;
        padding:0 8px;
    }
    .editNav li a{
        font-size: 0.70rem;
        color: rgba(102,102,102,0.6);
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
        .sidenav .editNav{
            display:block;
        }
        .nav-list {
            display: block;
        }
        .nav-item{
            margin-top: 16px;
            margin-bottom: 16px;
        }
        .sidenav .editNav{
            display:block;
        }
    }
</style>