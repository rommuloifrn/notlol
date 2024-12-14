<script>
let nickName = $state('')
let tagLine = $state('')

</script>

<h1>notlol</h1>
<ul>
    <li>{nickName} / {tagLine}</li>
</ul>
<!-- https://svelte.dev/tutorial/svelte/text-inputs -->
<form>
    <input bind:value={nickName} placeholder="nick" />
    <input bind:value={tagLine} type="text" name="" id="" placeholder="tagLine"/>
    <button>Check</button>
</form>
