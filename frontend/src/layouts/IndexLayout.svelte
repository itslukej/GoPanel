<Head/>

<div class="wrapper">
  <Sidebar referralShow=true referralLink="https://www.digitalocean.com?refcode=371f56712ea4" name="{name}"
           avatar="{avatar}"/>
  <div class="super-container">
    <LoadingScreen/>
    <NotifyModal/>
    <div class="content-container" class:hide={$loadingScreen}>
      <Route {currentRoute} {params}/>
    </div>
  </div>
</div>

<script>
    import {Route} from 'svelte-router-spa'
    import Head from '../includes/Head.svelte'
    import Sidebar from '../includes/Sidebar.svelte'
    import LoadingScreen from '../includes/LoadingScreen.svelte'
    import NotifyModal from '../includes/NotifyModal.svelte'
    import axios from "axios";
    import {API_URL} from '../js/constants'
    import {notifyError} from '../js/util'
    import {loadingScreen} from "../js/stores"
    import {redirectLogin, setDefaultHeaders} from '../includes/Auth.svelte'

    export let currentRoute;
    export let params = {};

    setDefaultHeaders()

    let name;
    let avatar;

    async function loadData() {
        const res = await axios.get(`${API_URL}/api/session`);
        if (res.status !== 200) {
            if (res.data.auth === true) {
                redirectLogin();
            }

            notifyError(res.data.error);
            return;
        }

        name = res.data.username;
        avatar = res.data.avatar;
    }

    loadData();
</script>

<style>
    body {
        padding: 0 !important;
    }

    .wrapper {
        display: flex;
        width: 100%;
        height: 100%;
        margin: 0 !important;
        padding: 0 !important;
    }

    .super-container {
        display: flex;
        width: 100%;
        height: 100%;
    }

    .content-container {
        display: flex;
        width: 100%;
        height: 100%;
    }

    .hide {
        visibility: hidden;
    }

    @media (max-width: 950px) {
        .wrapper {
            flex-direction: column;
        }
    }
</style>