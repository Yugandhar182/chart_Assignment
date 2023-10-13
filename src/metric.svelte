<script>
    import { Card } from 'flowbite-svelte';
   
   
   
     let apiKey = "TEST45684CB2A93F41FC40869DC739BD4D126D77";
     let startDate = "01/01/2023";
     let endDate = "11/10/2023";
   
     const apiUrl = `https://api.recruitly.io/api/dashboard/ats/metrics?start=${startDate}&end=${endDate}&apiKey=${apiKey}`;
   
     let metrics = null;
   
     import { onMount } from 'svelte';
   
     onMount(async () => {
       try {
         const response = await fetch(apiUrl);
         if (response.ok) {
           metrics = await response.json();
         } else {
           console.error("Failed to fetch data");
         }
       } catch (error) {
         console.error("Error: " + error);
       }
     });
   </script>
   
   {#if metrics}
   
   <div class="container">
     <div class="card1">
     <Card >
       <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{metrics.totalJobs}</h5>
       <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight"> Jobs</p>
     </Card>
   </div>
    
     <div class="card2">
     <Card  >
       
       <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{metrics.totalPlacements}</h5>
      
       <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">Placements</p>
     </Card>
   </div>
     <div class="card3">
     <Card style="background-color:  rgb(84, 97, 243)" >
       <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">GBP{metrics.totalCommission}</h5>
       <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">Billing</p>
     </Card>
     </div>
     <div class="card4">
     <Card >
       <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{metrics.totalAdverts}</h5>
       <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">Adverts</p>
     </Card>
   </div>
     <div class="card5">
     <Card >
       <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{metrics.avgTimeToFillDays}</h5>
       <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">TTF</p>
     </Card>
     </div>
     <div class="card6">
     <Card >
       <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{metrics.avgCandidatesPerPlacement}</h5>
       <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight"> Candidates/Jobs</p>
     </Card>
   </div>
   </div>
   {/if}
   
   
   
   <style>
   
   
     .container {
       display: flex;
       flex-direction: row;
       padding: 20px;
       background-color: white;
       margin-top:70px;
       margin-left: 40px;
       width: 1400PX;
       height:170px ;
       margin-top:90px;
     }
     
     .card1{
     
       height: 20px;
       width: 200px;
       margin-left:5px;
      
      
     }
    
     .card2{
     
       height: 20px;
       width: 200px;
       margin-left: 50px;
      
     }
     .card3{
      
       height: 20px;
       width: 200px;
       margin-left: 30px;
      
     }
     .card4{
    
       height: 20px;
       width: 200px;
       margin-left:30px;
      
     }
     .card5{
     
       height: 20px;
     
       width: 200px;
       margin-left: 30px;
      }
     .card6{
     
       height: 20px;
       margin-left: 30px;
      width: 200px;
     }
   </style>