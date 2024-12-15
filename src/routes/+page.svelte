<script lang="ts">
    import { browser } from "$app/environment";
    import axios from "axios";
    let nickName = $state('')
    let tagLine = $state('')
    let history: any[] = $state([])

    updateHistory();

        /**
         * @param {any} n
         * @param {any} tl
         */
    async function getData() {
        console.log("start");
        
        putOnMainElement("")
        loadingIconSwitch()
        
        let endpoint = `http://localhost:8080/main?gameName=${nickName}&tagLine=${tagLine}`;
        try {
            const response: any = await axios.get(endpoint);

            putOnMainElement(
                `${response.data} days without playing!`
            );
            saveOnHistory(nickName, tagLine);
        } catch (error) {
            console.log(error);
        }
        
        
         

        loadingIconSwitch()
        console.log("finish");
        updateHistory();
        return null;
    }

    function putOnMainElement(text:any) {
        const daysElement = document.getElementById('days');
        daysElement!.innerHTML = text;
    }

    function loadingIconSwitch() {
        const loadingIcon = document.getElementById('loadingicon');
        loadingIcon!.hidden = !loadingIcon!.hidden;
        
    }

    function saveOnHistory(gameName:string, tagLine:string) {
        if (localStorage.getItem('history') == null)
            localStorage.setItem('history', JSON.stringify(
                [{'gameName':gameName, 'tagLine':tagLine}]
            ));
        else {
            let array: Object[] = JSON.parse(
                localStorage.getItem('history')!
            )

            if (array.find((element:any)=>{
                element.gameName == gameName;
            })) {

            } else {
                array.push(
                    {'gameName':gameName, 'tagLine':tagLine}
                )
                localStorage.setItem('history', JSON.stringify(array));
            }

            
        }
    }

    function updateHistory() {
        if(browser) {
            history = JSON.parse(
                localStorage.getItem('history')!
            )
            history = history.reverse()
        }
    }

    function clearHistory() {
        localStorage.setItem(
            'history',
            JSON.stringify([])
        );
        updateHistory();
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
        <img id="loadingicon" class="h-6 mx-auto" hidden src="loading.gif" alt="">
        <!-- https://svelte.dev/tutorial/svelte/text-inputs -->
        <form onsubmit={()=>{getData}}>
            <input class="focus:outline-none bg-transparent" bind:value={nickName} placeholder="player name" />
            <span class="text-zinc-500">#</span><input class="focus:outline-none bg-transparent" bind:value={tagLine} type="text" name="" id="" placeholder="tagLine"/> <br>
            <button type="submit" class="font-semibold bg-red-500 shadow-zinc-900 shadow-lg text-white hover:bg-red-600 transition mt-5 w-full py-2 px-3 text-xl rounded-md" onclick={getData}>Check</button>
        </form>
        <div class="mt-10">
            <span class="text-xl font-semibold">
                search history <br> <button class="text-zinc-400 font-normal text-sm hover:underline" onclick={clearHistory}>clear</button>
            </span>
            <ul>
                {#each history as player}
                <li>{player.gameName}#{player.tagLine}</li>
                {/each}
            </ul>
        </div>
    </div>
    
    
</div>