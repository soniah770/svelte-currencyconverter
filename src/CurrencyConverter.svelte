<script lang="ts">

    let firstAmount = 0.00;
    let convertFrom = 'NOK';
    let lastAmount = 0.00;
    let convertTo = '';
	let Apikey = '0f19f0d65512ec902fae';

    let currencyList = [
        {name : "NOK", desc:"NOK"},
        {name:"IRR", desc:"IRR"},
       
    ];

    async function convertCurrency() {

        let convertKey = convertFrom + '_' + convertTo;
        let url = "https://free.currconv.com/api/v7/convert?q=" + convertKey + "&compact=ultra&apiKey=Apikey";

        await fetch(url).then( response => {
            return response.json()
        })
        .then( data => {
            let rate = data[convertKey]

        lastAmount = rate * firstAmount
        })
    }

</script>

<div class="grid grid-rows-2">
 <div class="w-fullm bg-[#eb5f57] h-[500px] -z-[800] " >

    <div id="currency-converter" class="flex flex-col 
                    items-center justify-center">

        <select class="px-4 py-5 rounded-full border-[#eb5f57] appearance-none bg-[#eb5f57] text-5xl text-white" bind:value={convertFrom} >
            {#each currencyList as cl }
                <option value="{cl.name}">
                    {cl.desc}
                </option>
            {/each}
        </select>
          
       <br>
       <br/>

        <input class="text-2xl text-white border-none
        mr-3 mt-8 py-5 px-4 h-2 border
         rounded mb-2 appearance-none bg-[#eb5f57]" type="number" name="currencyAmount" placeholder="Enter Amount" bind:value="{firstAmount}" />
        <br /> <br/>

       
    </div>
 

   
</div>
<div class="flex flex-col 
items-center justify-center py-[100px] relative z-[800]">
 <button class="rounded-full border-[#eb5f57] bg-[#fff] border-8  outline-[#eb5f57] outline-4">
     <svg xmlns="http://www.w3.org/2000/svg" class="h-25 w-28 stroke-[#eb5f57]" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3"  >
         <path stroke-linecap="round" stroke-linejoin="round" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
       </svg>
     </button>
</div>
    <div  class="flex flex-
     items-center justify-center bg-[#faf8f9]" >

    <br /> 

    <select class="px-4 py-5 rounded-full text-5xl text-[#eb5f57] border-[#faf8f9] appearance-none bg-[#faf8f9] " bind:value={convertTo} on:change="{convertCurrency}" >
        {#each currencyList as cl }
            <option value="{cl.name}">
                {cl.desc}
            </option>
        {/each}
    </select>
    

    
    <br/>
    </div>
</div>

