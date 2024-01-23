<script>
    import { onMount } from 'svelte';
    import CardWrapper from '../components/CardWrapper.svelte';
    import Self from "../components/Self.svelte"

    // export let data
    let self = null, liker = null, recs = null

    let modal, tokentext, token, loadingmodal;

    function close(){
        if(tokentext.value.length != 0){
            modal.removeAttribute("open")
            getData(token)
        }
        else
            alert("Please enter your token to continue!")
    }

    async function getData(token){
        // loadingmodal.addAttribute('open', 'open')
        const _self = await fetch(
        "https://happned.onrender.com",
            {
                method: 'POST',
                body: "OAuth=\"eyJhbGciOiJIUzI1NiJ9.eyJzY29wZSI6WyJ1c2VyX2RlbGV0ZSIsInVzZXJfcmVwb3J0X3JlYWQiLCJ1c2VyX3RyYWl0X2Fuc3dlcl93cml0ZSIsInVzZXJfdXBkYXRlIiwiYm9vc3RfY3JlYXRlIiwiYm9vc3RfcmVhZCIsInVzZXJfc29jaWFsX2RlbGV0ZSIsInVzZXJfY29udmVyc2F0aW9uX3JlYWQiLCJ1c2VyX2FjY2VwdGVkX3JlYWQiLCJ1c2VyX2NvbnZlcnNhdGlvbl9jcmVhdGUiLCJhbGxfdXNlcl90cmFpdF9hbnN3ZXJfcmVhZCIsInVzZXJfcmVqZWN0ZWRfY3JlYXRlIiwidXNlcl9ibG9ja2VkX3JlYWQiLCJzaG9ydGxpc3RfcmVhZCIsInVzZXJfcmVwb3J0X3VwZGF0ZSIsInVzZXJfYWNoaWV2ZW1lbnRfcmVhZCIsInJld2FyZGVkX2Fkc191cGRhdGUiLCJ1c2VyX2FjaGlldmVtZW50X2RlbGV0ZSIsInVzZXJfcmVwb3J0X2RlbGV0ZSIsInVzZXJfYXVkaW9jYWxsX2NyZWF0ZSIsInVzZXJfYWNoaWV2ZW1lbnRfdXBkYXRlIiwidXNlcl92aWRlb2NhbGxfdXBkYXRlIiwidXNlcl9hcHBsaWNhdGlvbnNfcmVhZCIsInVzZXJfYmxvY2tlZF9kZWxldGUiLCJ1c2VyX3N1YnNjcmlwdGlvbl9jcmVhdGUiLCJwYWNrX3JlYWQiLCJ1c2VyX29yZGVyX3VwZGF0ZSIsInVzZXJfcmVhZCIsIm5vdGlmaWNhdGlvbl90eXBlX3JlYWQiLCJ1c2VyX2FjaGlldmVtZW50X2NyZWF0ZSIsInVzZXJfbWVzc2FnZV9yZWFkIiwidXNlcl9pbWFnZV9jcmVhdGUiLCJ1c2VyX2NvbnZlcnNhdGlvbl9kZWxldGUiLCJ1c2VyX3NvY2lhbF91cGRhdGUiLCJ1c2VyX2RldmljZV9kZWxldGUiLCJ1c2VyX2FjY2VwdGVkX2NyZWF0ZSIsInN1YnNjcmlwdGlvbl90eXBlX3JlYWQiLCJ1c2VyX3Bva2VfY3JlYXRlIiwidHJhaXRfcmVhZCIsInVzZXJfYXBwbGljYXRpb25zX3VwZGF0ZSIsInVzZXJfcmVwb3J0X2NyZWF0ZSIsInVzZXJfb3JkZXJfY3JlYXRlIiwidXNlcl9kZXZpY2VfdXBkYXRlIiwidXNlcl9zaG9wX3JlYWQiLCJhcmNoaXZlX2NyZWF0ZSIsInVzZXJfcmVqZWN0ZWRfcmVhZCIsInVzZXJfYXBwbGljYXRpb25zX2RlbGV0ZSIsInVzZXJfc3Vic2NyaXB0aW9uX2RlbGV0ZSIsInVzZXJfYXVkaW9jYWxsX3JlYWQiLCJ1c2VyX3N1YnNjcmlwdGlvbl9yZWFkIiwidXNlcl92aWRlb2NhbGxfcmVhZCIsInVzZXJfYmxvY2tlZF9jcmVhdGUiLCJ1c2VyX3N1YnNjcmlwdGlvbl91cGRhdGUiLCJ1c2VyX21lc3NhZ2VfY3JlYXRlIiwidXNlcl9tZXNzYWdlX2RlbGV0ZSIsInVzZXJfbW9kZV9yZWFkIiwidXNlcl9zb2NpYWxfY3JlYXRlIiwidXNlcl9pbWFnZV91cGRhdGUiLCJsb2NhbGVfcmVhZCIsInVzZXJfbm90aWZpY2F0aW9uc19yZWFkIiwiYWNoaWV2ZW1lbnRfdHlwZV9yZWFkIiwic2VhcmNoX3VzZXIiLCJ1c2VyX2ltYWdlX2RlbGV0ZSIsInVzZXJfZGV2aWNlX3JlYWQiLCJhbGxfdXNlcl9yZWFkIiwicmV3YXJkZWRfYWRzX3JlYWQiLCJ1c2VyX3NvY2lhbF9yZWFkIiwiYXJjaGl2ZV9yZWFkIiwidXNlcl9kZXZpY2VfY3JlYXRlIiwidXNlcl9wb3NpdGlvbl9yZWFkIiwicGF5bWVudF9wb3J0YWxfcmVhZCIsInVzZXJfYWNjZXB0ZWRfZGVsZXRlIiwidXNlcl9tZXNzYWdlX3VwZGF0ZSIsInVzZXJfYXVkaW9jYWxsX3VwZGF0ZSIsInVzZXJfb3JkZXJfcmVhZCIsInVzZXJfdmlkZW9jYWxsX2NyZWF0ZSIsImxhbmd1YWdlX3JlYWQiLCJhbGxfaW1hZ2VfcmVhZCIsInVzZXJfY29udmVyc2F0aW9uX3VwZGF0ZSIsInVzZXJfaW1hZ2VfcmVhZCIsImNoZWNrb3V0X2NyZWF0ZSIsInVzZXJfcmVqZWN0ZWRfZGVsZXRlIiwicmVwb3J0X3R5cGVfcmVhZCIsInVzZXJfcG9zaXRpb25fdXBkYXRlIl0sImp0aSI6ImM3ZmY2YWE1LTAyYTYtNDI5NC05YWQwLWZhNmZhZmYzMjZiNyIsInN1YiI6IjJkYjZiMWU2LTczZmItNGExMC04M2UzLTZiNWY5ZmExM2RjZSIsImF1ZCI6IlNxSFNQcW02anlvRlhTMnNBaEU2TmNjNUR2azlYUWp4MG1Ud2x3Q0tMdCIsImV4cCI6MTcwNjExNDg3OSwiaWF0IjoxNzA2MDI4NDc5fQ._1T4fSUVD7T_BMoGnK8fKTTG6jGNchn9svNlSA6EJlA\""
            }
        )
        const _recs = await fetch(
        "https://happned.onrender.com/recs",
            {
                method: 'POST',
                body: "OAuth=\"eyJhbGciOiJIUzI1NiJ9.eyJzY29wZSI6WyJ1c2VyX2RlbGV0ZSIsInVzZXJfcmVwb3J0X3JlYWQiLCJ1c2VyX3RyYWl0X2Fuc3dlcl93cml0ZSIsInVzZXJfdXBkYXRlIiwiYm9vc3RfY3JlYXRlIiwiYm9vc3RfcmVhZCIsInVzZXJfc29jaWFsX2RlbGV0ZSIsInVzZXJfY29udmVyc2F0aW9uX3JlYWQiLCJ1c2VyX2FjY2VwdGVkX3JlYWQiLCJ1c2VyX2NvbnZlcnNhdGlvbl9jcmVhdGUiLCJhbGxfdXNlcl90cmFpdF9hbnN3ZXJfcmVhZCIsInVzZXJfcmVqZWN0ZWRfY3JlYXRlIiwidXNlcl9ibG9ja2VkX3JlYWQiLCJzaG9ydGxpc3RfcmVhZCIsInVzZXJfcmVwb3J0X3VwZGF0ZSIsInVzZXJfYWNoaWV2ZW1lbnRfcmVhZCIsInJld2FyZGVkX2Fkc191cGRhdGUiLCJ1c2VyX2FjaGlldmVtZW50X2RlbGV0ZSIsInVzZXJfcmVwb3J0X2RlbGV0ZSIsInVzZXJfYXVkaW9jYWxsX2NyZWF0ZSIsInVzZXJfYWNoaWV2ZW1lbnRfdXBkYXRlIiwidXNlcl92aWRlb2NhbGxfdXBkYXRlIiwidXNlcl9hcHBsaWNhdGlvbnNfcmVhZCIsInVzZXJfYmxvY2tlZF9kZWxldGUiLCJ1c2VyX3N1YnNjcmlwdGlvbl9jcmVhdGUiLCJwYWNrX3JlYWQiLCJ1c2VyX29yZGVyX3VwZGF0ZSIsInVzZXJfcmVhZCIsIm5vdGlmaWNhdGlvbl90eXBlX3JlYWQiLCJ1c2VyX2FjaGlldmVtZW50X2NyZWF0ZSIsInVzZXJfbWVzc2FnZV9yZWFkIiwidXNlcl9pbWFnZV9jcmVhdGUiLCJ1c2VyX2NvbnZlcnNhdGlvbl9kZWxldGUiLCJ1c2VyX3NvY2lhbF91cGRhdGUiLCJ1c2VyX2RldmljZV9kZWxldGUiLCJ1c2VyX2FjY2VwdGVkX2NyZWF0ZSIsInN1YnNjcmlwdGlvbl90eXBlX3JlYWQiLCJ1c2VyX3Bva2VfY3JlYXRlIiwidHJhaXRfcmVhZCIsInVzZXJfYXBwbGljYXRpb25zX3VwZGF0ZSIsInVzZXJfcmVwb3J0X2NyZWF0ZSIsInVzZXJfb3JkZXJfY3JlYXRlIiwidXNlcl9kZXZpY2VfdXBkYXRlIiwidXNlcl9zaG9wX3JlYWQiLCJhcmNoaXZlX2NyZWF0ZSIsInVzZXJfcmVqZWN0ZWRfcmVhZCIsInVzZXJfYXBwbGljYXRpb25zX2RlbGV0ZSIsInVzZXJfc3Vic2NyaXB0aW9uX2RlbGV0ZSIsInVzZXJfYXVkaW9jYWxsX3JlYWQiLCJ1c2VyX3N1YnNjcmlwdGlvbl9yZWFkIiwidXNlcl92aWRlb2NhbGxfcmVhZCIsInVzZXJfYmxvY2tlZF9jcmVhdGUiLCJ1c2VyX3N1YnNjcmlwdGlvbl91cGRhdGUiLCJ1c2VyX21lc3NhZ2VfY3JlYXRlIiwidXNlcl9tZXNzYWdlX2RlbGV0ZSIsInVzZXJfbW9kZV9yZWFkIiwidXNlcl9zb2NpYWxfY3JlYXRlIiwidXNlcl9pbWFnZV91cGRhdGUiLCJsb2NhbGVfcmVhZCIsInVzZXJfbm90aWZpY2F0aW9uc19yZWFkIiwiYWNoaWV2ZW1lbnRfdHlwZV9yZWFkIiwic2VhcmNoX3VzZXIiLCJ1c2VyX2ltYWdlX2RlbGV0ZSIsInVzZXJfZGV2aWNlX3JlYWQiLCJhbGxfdXNlcl9yZWFkIiwicmV3YXJkZWRfYWRzX3JlYWQiLCJ1c2VyX3NvY2lhbF9yZWFkIiwiYXJjaGl2ZV9yZWFkIiwidXNlcl9kZXZpY2VfY3JlYXRlIiwidXNlcl9wb3NpdGlvbl9yZWFkIiwicGF5bWVudF9wb3J0YWxfcmVhZCIsInVzZXJfYWNjZXB0ZWRfZGVsZXRlIiwidXNlcl9tZXNzYWdlX3VwZGF0ZSIsInVzZXJfYXVkaW9jYWxsX3VwZGF0ZSIsInVzZXJfb3JkZXJfcmVhZCIsInVzZXJfdmlkZW9jYWxsX2NyZWF0ZSIsImxhbmd1YWdlX3JlYWQiLCJhbGxfaW1hZ2VfcmVhZCIsInVzZXJfY29udmVyc2F0aW9uX3VwZGF0ZSIsInVzZXJfaW1hZ2VfcmVhZCIsImNoZWNrb3V0X2NyZWF0ZSIsInVzZXJfcmVqZWN0ZWRfZGVsZXRlIiwicmVwb3J0X3R5cGVfcmVhZCIsInVzZXJfcG9zaXRpb25fdXBkYXRlIl0sImp0aSI6ImM3ZmY2YWE1LTAyYTYtNDI5NC05YWQwLWZhNmZhZmYzMjZiNyIsInN1YiI6IjJkYjZiMWU2LTczZmItNGExMC04M2UzLTZiNWY5ZmExM2RjZSIsImF1ZCI6IlNxSFNQcW02anlvRlhTMnNBaEU2TmNjNUR2azlYUWp4MG1Ud2x3Q0tMdCIsImV4cCI6MTcwNjExNDg3OSwiaWF0IjoxNzA2MDI4NDc5fQ._1T4fSUVD7T_BMoGnK8fKTTG6jGNchn9svNlSA6EJlA\""
            }
        )
        self = await _self.json()
        liker = self.liker
        recs = await _recs.json()
        // loadingmodal.removeAttribute('open')
    }

    onMount(() => {
        modal = document.getElementById('tokenmodal')
        tokentext = document.getElementById('tokendata')
        loadingmodal = document.getElementById('loadingmodal')
    })
</script>

<dialog id="tokenmodal" open>
    <article>
      <h3>Enter Your Token</h3>
      <textarea id="tokendata" bind:value={token}></textarea>
      <footer>
        <button on:click={close}>Submit</button>
      </footer>
    </article>
</dialog>
<dialog id="loadingmodal">
    <a href="#" aria-busy="true">Fetching data, please wait…</a>
</dialog>

<h1>Happn-Ed</h1>

<h1>Self</h1>
<Self {self} {liker}/>
<h1>Recommendations</h1>
<CardWrapper cards={recs}/>