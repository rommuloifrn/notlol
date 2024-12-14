<script lang="ts">
    import axios from "axios";
    let nickName = $state('')
    let tagLine = $state('')

        /**
         * @param {any} n
         * @param {any} tl
         */
    async function getData() {
        console.log("start");
        
        let endpoint = `http://localhost:8080/main?gameName=${nickName}&tagLine=${tagLine}`;
        const response: any = await axios.get(endpoint);
        const daysElement = document.getElementById('days');

        daysElement!.innerHTML = `${response.data} days without playing!`;
        console.log("finish");
        return null;
    
}

</script>

<style>
    :global(body) {
        height: 100vh;
    }
</style>

<div class="h-full flex justify-center pt-[30vh] text-center text-zinc-200 bg-zinc-800">
    <div>
        <h1 class="font-bold text-2xl">notlol</h1>
        <!-- <ul>
            <li>{nickName}  #{tagLine}</li>
        </ul> -->
        <div id="days">
            search some player!
        </div>
        <!-- https://svelte.dev/tutorial/svelte/text-inputs -->
        <form onsubmit={()=>{getData}}>
            <input class="focus:outline-none bg-transparent" bind:value={nickName} placeholder="player name" />
            <span class="text-zinc-500">#</span><input class="focus:outline-none bg-transparent" bind:value={tagLine} type="text" name="" id="" placeholder="tagLine"/> <br>
            <button class="font-semibold bg-red-500 text-white hover:bg-red-600 transition mt-5 w-full py-2 px-3 text-xl rounded-md" onclick={getData}>Check</button>
        </form>
    </div>
    
</div>