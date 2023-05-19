<script lang="ts">

</script>

<main class="container">
    <article>
        <header>
            <h1>Register</h1>
        </header>
        <form class="container" action="?/register" method="POST">
            <div class="grid">
                <label for="email">
                    Email
                    <input type="text" name="email" id="email" />
                </label>
            </div>
    
            <div class="grid">
                <label for="password">
                    Password
                    <input type="password" name="password" id="password" />
                </label>
            </div>
            <button>Register</button>
        </form>
    </article>
</main>