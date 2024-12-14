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

<h1>notlol</h1>
<!-- <ul>
    <li>{nickName}  #{tagLine}</li>
</ul> -->
<div id="days">
    search some player!
</div>
<!-- https://svelte.dev/tutorial/svelte/text-inputs -->
<form>
    <input bind:value={nickName} placeholder="nick" />
    #<input bind:value={tagLine} type="text" name="" id="" placeholder="tagLine"/>
    <button onclick={getData}>Check</button>
</form>
