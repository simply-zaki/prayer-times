<script>
  let is_settings_open = $state(false)
  let method = $state(localStorage.getItem("method") || "0")
  let date = new Date().getMonth() +1
  console.log(date)
  $effect(()=>{
    localStorage.setItem("method",method)
  })
  let aladhan_obj = {}
  async function get_times(){
  }
  get_times()
</script>

<main class="bg-green-500 relative w-screen h-screen overflow-hidden">
    <h1 class="text-4xl text-center my-4">أوقات الصلاة</h1>
    <button onclick={()=>{ is_settings_open = !is_settings_open}}>
    <img class="size-10 absolute top-5 left-5 cursor-pointer" src="src/imgs/settings.svg" alt="settings">
    </button>
</main>
{#if is_settings_open}
    <div class="absolute top-1/2 text-zinc-300 left-1/2 border p-4 rounded-lg border-zinc-700 bg-zinc-800 flex flex-col items-center -translate-x-1/2 -translate-y-1/2 gap-4">
        <label class="-mb-4" for="method">Method</label>
        <select  bind:value={method} id="method" class="border text-center border-neutral-700 outline-0 rounded-lg py-2">
            <option class='bg-zinc-800' value="0">Jafari / Shia Ithna-Ashari</option>
            <option class='bg-zinc-800' value="1">University of Islamic Sciences, Karachi</option>
            <option class='bg-zinc-800' value="2">Islamic Society of North America</option>
            <option class='bg-zinc-800' value="3">Muslim World League</option>
            <option class='bg-zinc-800' value="4">Umm Al-Qura University, Makkah</option>
            <option class='bg-zinc-800' value="5">Egyptian General Authority of Survey</option>
            <option class='bg-zinc-800' value="7">Institute of Geophysics, University of Tehran</option>
            <option class='bg-zinc-800' value="8">Gulf Region</option>
            <option class='bg-zinc-800' value="9">Kuwait</option>
            <option class='bg-zinc-800' value="10">Qatar</option>
            <option class='bg-zinc-800' value="11">Majlis Ugama Islam Singapura, Singapore</option>
            <option class='bg-zinc-800' value="12">Union Organization islamic de France</option>
            <option class='bg-zinc-800' value="13">Diyanet İşleri Başkanlığı, Turkey</option>
            <option class='bg-zinc-800' value="14">Spiritual Administration of Muslims of Russia</option>
            <option class='bg-zinc-800' value="15">Moonsighting Committee Worldwide</option>
            <option class='bg-zinc-800' value="16">Dubai (experimental)</option>
            <option class='bg-zinc-800' value="17">Jabatan Kemajuan Islam Malaysia (JAKIM)</option>
            <option class='bg-zinc-800' value="18">Tunisia</option>
            <option class='bg-zinc-800' value="19">Algeria</option>
            <option class='bg-zinc-800' value="20">KEMENAG - Kementerian Agama Republik Indonesia</option>
            <option class='bg-zinc-800' value="21">Morocco</option>
            <option class='bg-zinc-800' value="22">Comunidade Islamica de Lisboa</option>
            <option class='bg-zinc-800' value="23">Ministry of Awqaf, Islamic Affairs and Holy Places, Jordan</option>
        </select>
    </div>
{/if}
