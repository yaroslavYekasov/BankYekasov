<script context="module">
    export async function preload({ params }, { token }) {
        if (!token) {
            this.redirect(302, `/login`);
        }
    }
</script>
<script>
    import {post} from "utils.js";
    async function getMyData(){

        return await post(`auth/getMyData`).then(r => {
            r.funds = r.accounts.reduce((funds, account) => funds + account.balance, 0)
            return r
        })
    }

    async function getTransactions(){

        return await post(`auth/getTransactions`)
    }
</script>
{#if process.browser}
{#await getMyData()}
    Loading...
    {:then my}
    <p>
        {my.name}
    </p>
    <pre>{JSON.stringify(my, null, 4)}</pre>
{/await}
    {/if}