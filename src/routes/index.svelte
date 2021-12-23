<script type="ts">
    import { writable } from 'svelte/store';
    //Starting Value;
    let base = 650000;
    //Yield Rate
    let yr = 6
    //Withdrawl rate
    let wr = 4;
    //Years
    let years = 20;

    
    let yearlybase = writable([]);
    let yearlywithdrawls = writable([]);
    
    const calc= ()=>{
        
        let currentValue = base;
        let wrp = wr/100;
        let yrp = yr/100;
        $yearlywithdrawls = [];
        $yearlybase = [];
        //iterate;
        for(var i=0; i<years; i++){
            //Increase by specified ammount
            currentValue*=1+yrp;
            //Withdraw
            currentValue-=currentValue*wrp;
            
            $yearlywithdrawls = [... $yearlywithdrawls, (Math.round(currentValue* wrp * 100) / 100).toFixed(2)]
            $yearlybase = [... $yearlybase, (Math.round(currentValue * 100) / 100).toFixed(2)];
        }
    }
    calc();
</script>
<form method="post" id="calculator" on:submit|preventDefault={calc} class="p-8">
    <div class="columns-2">
        <div class="form-control mb-4">
            <label class="" for="base">Starting Base</label>
            <input type="number" name="base" id="base" bind:value={base}  class="input input-bordered" on:keyup="{calc}"/>
        </div>
        <div class="form-control mb-4">
            <label class="" for="years">Years</label>
            <input type="number" name="base" id="years" bind:value={years} class="input input-bordered" on:keyup="{calc}"/>
        </div>
        <div class="form-control mb-4">
            <label class="" for="yield">Yearly Yield (as a %)</label>
            <input type="number" name="base" id="yield" bind:value={yr} class="input input-bordered" on:keyup="{calc}"/>
        </div>
        <div class="form-control mb-4">
            <label class="" for="yield">Yearly Withdraw (as a %)</label>
            <input type="number" name="base" id="wr" bind:value={wr} class="input input-bordered" on:keyup="{calc}"/>
        </div>
    </div>
    <button type="submit" class="btn">Calculate</button>
</form>
<style>
    table {
	    display: table;
    }
    table tr {
        display: table-cell;
    }
    table tr td {
        display: block;
    }
    table tr td:nth-child(odd){
        background-color: rgba(0, 0, 0, 0.025)
    }
    .th{
        font-weight:bold;
        min-width: 25vw;
    }
</style>
<table class="table m-10">
    <tr>
        <td class="th">Withdrawl</td>
        {#each $yearlywithdrawls as value}
            <td>${ value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",") }</td>
        {/each}
    </tr>
    <tr>
        <td class="th">Balance</td>
        {#each $yearlybase as ybase}
            <td>${ ybase.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",") }</td>
        {/each}
    </tr>
</table>