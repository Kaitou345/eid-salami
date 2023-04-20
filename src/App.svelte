<script>
import "./app.css";
import html2canvas from 'html2canvas';
import Check from "svelte-icons/fa/FaCheck.svelte"


let pfp = null;
let qr = null;
let capture = null;

let pfpCheck = false;
let qrCheck = false;


let pfpImage;
let qrImage;

let existingCanvas = null;

let hide = false;
let url = null;

function generate()
{
  html2canvas(capture, {canvas: existingCanvas}).then(function(canvas) {
    hide = true;
    document.body.appendChild(canvas);
    url = canvas.toDataURL()
    console.log(url)

});
}

function onPfpChange()
{
  const file = pfp.files[0];
		
    if (file) {
      const reader = new FileReader();
      reader.addEventListener("load", function () {
        pfpImage.setAttribute("src", reader.result);
      });
      reader.readAsDataURL(file);
			pfpCheck = true;
			return;
    } 
}

function onQrChange()
{
  const file = qr.files[0];
		
    if (file) {
      const reader = new FileReader();
      reader.addEventListener("load", function () {
        qrImage.setAttribute("src", reader.result);
      });
      reader.readAsDataURL(file);
			qrCheck = true;
			
			return;
    } 
}

</script>

<main class="m-0 p-0 font-sans">
  {#if !hide}
  <img src="bar.png" class="w-full" alt="">
  <div class="z-10 bar w-full">
  </div>
  <div class="relative my-10">
    <h1 class="text-center font-bold text-[#df126d] text-5xl">Create your Bkash সালামি poster</h1>
    <div>
      <form on:submit|preventDefault action="" class="flex flex-col gap-10 mt-10">

        <div class="flex flex-col gap-5  items-center justify-around">
          <label class="text-center font-medium text-2xl" for="picture">আপনার ছবি / Your picture</label>
          <label class="py-2 px-5 font-semibold rounded-2xl bg-[#df126d] text-center text-white flex gap-1" for="picture">Upload
            {#if pfpCheck }
            <div class="w-5 text-[#8fff66]">
              <Check />
            </div>
            {/if}
          </label>

          <input bind:this={pfp} on:change={onPfpChange} class="hidden" id="picture" type="file">
        </div>

        <div class="flex flex-col gap-5 items-center justify-around">
          <label class="text-center font-medium text-2xl" for="qr">QR কোড এর স্ক্রিনশট / QR Code Screenshot <br>
            <span class="text-[#df126d] text-base">( স্ক্রিনশট পেতে বিকাশ অ্যাপ এ গিয়ে নিজের ছবি তে চাপ দিন এবং স্ক্রিনশট তুলে কোডটি ক্রপ করুন )
            </span></label>
            <label class="py-2 px-5 font-semibold rounded-2xl bg-[#df126d] text-center text-white flex gap-1" for="qr">Upload
              {#if qrCheck }
              <div class="w-5 text-[#8fff66]">
                <Check />
              </div>

              {/if}
              
          </label>
          
          <input bind:this={qr} on:change={onQrChange} class="hidden " id="qr" type="file">
        </div>
        <div class="flex flex-col items-center justify-center">
          <button class="py-2 px-5 font-semibold rounded-2xl bg-green-600 text-center text-white" on:click={generate}>Create</button>
          {#if hide}
          <p>Right click and save the image</p>
          {/if}
        </div>
      </form>
    </div>
  </div>
  
  <div  id="capture" class:hidden={hide} class="absolute -left-[50000px] flex items-center justify-center">
    <div bind:this={capture} class="relative w-[1080px] h-[1080px] overflow-hidden scale-100" >
      <div>
        <img  bind:this={qrImage} class="object-contain absolute top-[490px] left-[200px] z-10 w-[260px] h-[260px]" alt="">
      </div>
      <div class="absolute rounded-r-[3.9rem] top-[366px] left-[592px] z-10 w-[424px] h-[440px] overflow-hidden object-cover">
        <img bind:this={pfpImage} class="absolute scale-125 object-cover" alt="">
      </div>
      <img  class="absolute object-contain w-full h-full" src="Bkash.png" alt="">
    </div>
  </div>
  <footer class="text-center text-sm mb-5" > 
    <p>
      Created by <span class="text-[#df126d]">Tanveer Nadim Arpon</span> & <span class="text-[#df126d]">Muhammad Seyan</span>
    </p>  
    <p>
    This website is made for experimental purposes only. We are not associated with Bkash in any capacity.

    </p>
  </footer>
{/if}  

  

</main>


<style>
  
</style>
