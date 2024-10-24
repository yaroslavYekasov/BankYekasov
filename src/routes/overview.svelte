<script context="module">
    export async function preload({ params }, { token }) {
        if (!token) {
            this.redirect(302, `/login`);
        }
    }
</script>
owawiu
