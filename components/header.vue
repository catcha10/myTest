<template>
    <header :class="[toggleSidebar==true ? 'open' : 'close']" >

        <div class="drawer-toggle" role="button" @click="$store.dispatch('nav/toggleSidebar')">
            <div class="bar"></div>
            <div class="bar"></div>
            <div class="bar"></div>
        </div>

        <div class="app-links">
            <app-links></app-links>
        </div>

    </header>
</template>

<script>
    import AppLinks from '~/components/appLinks'
export default {
    components: { AppLinks },
    computed: {
        toggleSidebar() {
            return this.$store.getters['nav/toggleSidebar']
        }
    }
}
</script>

<style scoped >
    header{
        display: grid;
        grid-template: 60px / auto 1fr;
        align-items: center;
        background-color: #3a77b2;
        transition: all 0.3s ease-out;
    }
    header.open{
      transform: translateX(300px);
    }
    .app-links{
        justify-self: end;
    }
    .brand-name {
        margin: 0 10px;
        font-size: 1.3rem;
    }
    .brand-name a {
        text-decoration: none;
        color: white;
    }
    .drawer-toggle .bar {
        width: 90%;
        height: 2px;
        background-color: white;
    }
    .drawer-toggle {
        display: flex;
        justify-self: end;
        flex-direction: column;
        justify-content: space-around;
        height: 50%;
        width: 30px;
        padding-right: 16px;
        cursor: pointer;
        margin-left:30px;
    }
    @media (max-width: 767px) and screen{
        header{
            padding: 0 16px;
        }
        header:nth-child{
            justify-self: end !important;
        }
        .app-links {
            display: none;
        }
    }
    @media (min-width: 768px) and screen{
        header{
            padding: 0 64px;
        }
        .app-links {
            display: block;
        }
        .drawer-toggle {
            display: none;
        }
    }
</style>