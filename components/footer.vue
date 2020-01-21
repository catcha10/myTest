<template>
    <footer>
        <div class="footerSide left" >
            <ul>
                <li><nuxt-link to="/" title=""  >Terms & condition</nuxt-link></li>
                <li><nuxt-link to="/" title=""  >Policy privacy</nuxt-link></li>
            </ul>
        </div> 
        <div class="footerSide right" ><p>&copy; Copyright 2020</p></div>
    </footer>
</template>

<style scoped>
    footer{
        background: #ccc;
        background-color:#3a77b2;
        color:#fff;
        display: flex;
        justify-content: space-between;
        padding:15px 20px;
    }
    footer p{
        margin:0px;
        font-size:0.8rem;
        font-family: helvetica;
        font-style: normal;
        font-weight: 300; 
    }
    .footerSide{
        width:50%;
        display:inline-block;
    }
    .footerSide.left{
        float:left;
    }
    .footerSide.right{
        float:right;
    }
    .footerSide ul{
        margin:0px;
        padding:0px;
        list-style:none;
        display:inline-block;
        overflow:hidden;
    }
    .footerSide ul li{
        float:left;
        padding-right:20px;
        margin-right:20px;
        border-right:1px solid rgba(255,255,255,0.8);
    }
    .footerSide ul li a{
        font-size:0.813rem;
        font-family: helvetica;
        font-style: normal;
        font-weight: 300; 
        color:#fff;
        text-decoration:none;
    }
    .footerSide ul li a:hover, .footerSide ul li a:focus{
        color:#fff;
        text-decoration:underline;
    }
    .footerSide ul li:last-child{
        border-right:none;
        padding-right:0px;
        margin-right:0px;
    }

    .footerSide.right{
        text-align:right;
    }

    @media (max-width:768px){
        footer{
            flex-direction: column;
        }
       .footerSide{
           width:100%;
       } 
       .footerSide.left {
           margin-bottom:10px;
           text-align:center;
       }
       .footerSide p{
           text-align:center;
       }
    }
</style>