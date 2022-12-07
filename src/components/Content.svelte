<script>
    let tweets = []
    let tweet_actual = ''

    function vaciarLocalStorage() {
        localStorage.removeItem('tweets')
        tweets = []
    }
    function eliminarTweet(index) {
        tweets.splice(index, 1)

        localStorage.setItem('tweets', JSON.stringify(tweets))
        tweets = tweets
    }

    function agregarTweetLocalStorage() {
        let setTweets
        setTweets = getTweetsLocalStorage()
        setTweets.push(tweet_actual)

        localStorage.setItem('tweets', JSON.stringify(setTweets))
        tweet_actual = ''
        // localStorage

        loadedTweets()
    }

    function getTweetsLocalStorage() {
        let getTweets

        if (localStorage.getItem("tweets") === null) {
            getTweets = []
        } else {
            getTweets = JSON.parse(localStorage.getItem("tweets"))
        }
        return getTweets
    }
    const loadedTweets = () => {
        tweets = getTweetsLocalStorage()
        console.log(tweets)
    }
</script>
<div class="container">
    <div class="blocks">
        <div class="block">
            <form class="form-control" on:submit|preventDefault={agregarTweetLocalStorage}>
                <label class="form-item" for="tweet">Tweet</label>
                <input class="form-item" type="text" name="tweet" id="tweet" required bind:value={tweet_actual}>
                <input class="button_aceptar" type="submit" value="Agregar">
                <input class="button_vaciar" type="button" value="Vaciar" on:click={vaciarLocalStorage}>
            </form>
        </div>
    
        <div class="block">
            <p>Mis Tweets</p>
            <ul>
                {#if tweets.length != 0}
                    {#each tweets as t,i}
                        <li class="list-item">
                            {t}
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <p on:click={ () => eliminarTweet(i) }>x</p>
                        </li>
                    {/each}
                {/if}
            </ul>
        </div>
    </div>
</div>
<style>
    .container {
        width: 65%;
        margin: 4rem auto;
    }
    
    .blocks {
        display: flex;
        column-gap: 1.5rem;
        justify-content: space-between;
    }
    .block {
        width: 50%;
    }
    .form-control {
        display: flex;
        flex-direction: column;
        row-gap: 12px;
    }
    label,
    input {
        font-size: 1.4rem;
    }
    input {
        width: 100%;
        padding: 10px;
        outline: none;
        border: 1px solid gray;
        border-radius: 5px;
    }
    input:focus {
        border: 1px solid rgb(49, 128, 247);
        box-shadow: 0 0 3px rgb(72, 141, 243);
    }
    .button_aceptar {
        background-color: rgb(47, 127, 247);
        color: white;
    }
    .button_vaciar {
        background-color: rgb(255, 37, 37);
        color: white;
    }
    p { text-align: center; font-size: 1.8rem; }
    ul {
        margin-top: 10px;
        font-size: 1.3rem;
    }
    .list-item {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .list-item p {
        color: red;
        font-weight: 500;
        cursor: pointer;
    }

    @media (max-width: 920px) {
        .container {
            width: 80%;
        }
    }
    @media (max-width: 768px) {
        .container {
            width: 90%;
        }
    }
    @media (max-width: 520px) {
        .container {
            width: 98%;
        }
        .blocks {
            flex-direction: column;
            row-gap: 2rem;
        }
        .block {
            width: 100%;
        }
    }
</style>