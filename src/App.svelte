<script>
  let is_settings_open = $state(false)
  let method = $state(localStorage.getItem("method") || "1")
  let date = new Date()
  let full_date = `${date.getDate()}-${date.getMonth() + 1}-${date.getFullYear()}`
  let aladhan_obj = $state()
  let current_prayer = $state("asr")
  let times = $state()
  let text_class = $derived(["fajr","maghrib","isha"].includes(current_prayer) ? "dark": "light")

  $effect(()=>{
    localStorage.setItem("method",method)
  })
  //checking the prayer every second
  setInterval(()=>{
    check_prayer()
  },1000)


  async function get_times(){
    var location = await fetch("https://freeipapi.com/api/json")
    var location_json = await location.json()
    aladhan_obj = await fetch(`https://api.aladhan.com/v1/timingsByAddress/${full_date}?address=${location_json.cityName}&method=${method}&timezonestring=${location_json.timeZones[0]}`)
    aladhan_obj = await aladhan_obj.json()
    times = aladhan_obj.data.timings
    check_prayer()
  }
  function check_prayer(){
    //updating time
        date = new Date()
        let time_in_miliseconds_redone_by_me_cuz_js_is_too_useless_to_handle_such_a_simple_task_like_why_give_me_time_since_1970_how_am_i_going_to_use_that = (date.getHours() * 3600000) + (date.getMinutes() * 60000)
        if (time_in_miliseconds_redone_by_me_cuz_js_is_too_useless_to_handle_such_a_simple_task_like_why_give_me_time_since_1970_how_am_i_going_to_use_that >= (parseInt(times.Isha.split(":")[0]) * 3600000) + (parseInt(times.Isha.split(":")[1]) * 60000) ){
          current_prayer = "isha"
          return
        }

        if (time_in_miliseconds_redone_by_me_cuz_js_is_too_useless_to_handle_such_a_simple_task_like_why_give_me_time_since_1970_how_am_i_going_to_use_that >= (parseInt(times.Maghrib.split(":")[0]) * 3600000) + (parseInt(times.Maghrib.split(":")[1]) * 60000) ){
          current_prayer = "maghrib"
          return
        }

        if (time_in_miliseconds_redone_by_me_cuz_js_is_too_useless_to_handle_such_a_simple_task_like_why_give_me_time_since_1970_how_am_i_going_to_use_that >= (parseInt(times.Asr.split(":")[0]) * 3600000) + (parseInt(times.Asr.split(":")[1]) * 60000) ){
          current_prayer = "asr"
          return
        }

        if (time_in_miliseconds_redone_by_me_cuz_js_is_too_useless_to_handle_such_a_simple_task_like_why_give_me_time_since_1970_how_am_i_going_to_use_that >= (parseInt(times.Dhuhr.split(":")[0]) * 3600000) + (parseInt(times.Dhuhr.split(":")[1]) * 60000) ){
          current_prayer = "dhuhr"
          return
        }

        if (time_in_miliseconds_redone_by_me_cuz_js_is_too_useless_to_handle_such_a_simple_task_like_why_give_me_time_since_1970_how_am_i_going_to_use_that >= (parseInt(times.Fajr.split(":")[0]) * 3600000) + (parseInt(times.Fajr.split(":")[1]) * 60000) ){
          current_prayer = "fajr"
          return
        }
  }

  get_times()
</script>


{#snippet prayer_time(prayer = "fajr",icon = "/imgs/fajr.svg",time= "5:00")}
    <div class="border  shadow-black shadow-md flex flex-col gap-1 items-center border-slate-700 text-slate-300  w-30 rounded-lg py-2 px-4" class:bg-slate-900={prayer.toLowerCase() !== current_prayer} class:bg-slate-700={prayer.toLowerCase() === current_prayer} class:scale-105={prayer.toLowerCase() === current_prayer}>
        <img src={icon} class="size-7" alt="prayer_time_icon">
        {prayer}
        <time class="text-sm opacity-50">{time}</time>
    </div>
{/snippet}

<main class={`${current_prayer} relative w-screen h-screen overflow-x-hidden`}>
    <h1 class={`text-4xl text-center my-4 ${text_class} `}  >Prayer times</h1>
    {#if times}
        <span class="flex flex-col gap-4 items-center">
        {@render prayer_time("Fajr","src/imgs/fajr.svg",times.Fajr)}
        {@render prayer_time("Dhuhr","src/imgs/dhuhr.svg",times.Dhuhr)}
        {@render prayer_time("Asr","src/imgs/asr.svg",times.Asr)}
        {@render prayer_time("Maghrib","src/imgs/maghrib.svg",times.Maghrib)}
        {@render prayer_time("Isha","src/imgs/isha.svg",times.Isha)}

        </span>
    {/if}
    <button onclick={()=>{ is_settings_open = !is_settings_open}}>
    <img class="size-10 absolute top-5 left-5 cursor-pointer" src="src/imgs/settings.svg" alt="settings">
    </button>
</main>
{#if is_settings_open}
    <div class="absolute top-1/2 text-slate-300 left-1/2  border p-4 rounded-lg border-zinc-700 bg-slate-900 flex flex-col items-center -translate-x-1/2 -translate-y-1/2 gap-4">
        <label class="-mb-4" for="method">Method</label>
        <select  bind:value={method} id="method" class="border text-center border-neutral-700 outline-0 rounded-lg py-2">
            <option class='bg-slate-900' value="1">Karachi</option>
            <option class='bg-slate-900' value="2">North America</option>
            <option class='bg-slate-900' value="3">Muslim World League</option>
            <option class='bg-slate-900' value="4">Makkah</option>
            <option class='bg-slate-900' value="5">Egypt</option>
            <option class='bg-slate-900' value="7">Tehran</option>
            <option class='bg-slate-900' value="8">Gulf Region</option>
            <option class='bg-slate-900' value="9">Kuwait</option>
            <option class='bg-slate-900' value="10">Qatar</option>
            <option class='bg-slate-900' value="11">Singapore</option>
            <option class='bg-slate-900' value="12">France</option>
            <option class='bg-slate-900' value="13">Turkey</option>
            <option class='bg-slate-900' value="14">Russia</option>
            <option class='bg-slate-900' value="15">Moonsighting Committee Worldwide</option>
            <option class='bg-slate-900' value="16">Dubai (experimental)</option>
            <option class='bg-slate-900' value="17">Malaysia</option>
            <option class='bg-slate-900' value="18">Tunisia</option>
            <option class='bg-slate-900' value="19">Algeria</option>
            <option class='bg-slate-900' value="20">Indonesia</option>
            <option class='bg-slate-900' value="21">Morocco</option>
            <option class='bg-slate-900' value="22">Lisboa</option>
            <option class='bg-slate-900' value="23">Jordan</option>
        </select>
    </div>
{/if}
