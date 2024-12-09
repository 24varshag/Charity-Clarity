<script>
  import { onMount } from 'svelte';
  import Popup from './CharityPopup.svelte';  
  import Swal from 'sweetalert2'

  let scrollY = 0;
  let isInfoClicked = false;
  let shadow;
  let isPopupVisible = false; // State to control the popup visibility
  let headerText = "Where's Teddy Hiding?"; // Default text for the header


  function openPopup() {
    isPopupVisible = true;  
  }

  function closePopup() {
    isPopupVisible = false;  
  }

  function handleInfoClick() {
  Swal.fire({
    title: "Ready for a fun challenge?",
    html: `
      This page is all about raising awareness for glaucoma, a sneaky eye condition you might not even know about!<br><br>
      Here's how to play:<br><br>
      <strong>1. Find the Teddy:</strong> Scroll through the page and try to find the hidden teddy bear. It's trickier than it looks!<br><br>
      <strong>2. Learn About Glaucoma:</strong> Once you find the teddy, you'll unlock important information about glaucoma.<br><br>
      <strong>3. Support the Cause:</strong> We'll also show you how to support organizations that are fighting glaucoma.
    `,
    icon: "question",
  });
}



  function handleScroll(event) {
    scrollY = window.scrollY;
    const styleSheet = document.styleSheets[0]; 

  if (scrollY > 0) {
    styleSheet.insertRule(`
      body::before {  
        filter: blur(0px);
      }
    `, styleSheet.cssRules.length);
  } 
    
  }

  // Reactive variable to determine if the header should be resized
  $: isSmall = scrollY > 10;
  $: headerText = isSmall ? "Your Task: Find Where Teddy's Hiding 🧸 " : "Where's Teddy Hiding?"; 

  let teddyPosition = {
    top: "0px",
    left: "0px"
  };
  // Moves the shadow div with the cursor
  onMount(() => {
    const shadow = document.querySelector('.shadow');

    document.addEventListener('mousemove', (e) => {
      let x = e.clientX - (document.documentElement.clientWidth * 1.5);
      let y = e.clientY - (document.documentElement.clientHeight * 1.5) + 100;
      shadow.style.transform = 'translate(' + x + 'px, ' + y + 'px)';
    });

   
    const randomTop = Math.random() * (window.innerHeight - 100); 
    const randomLeft = Math.random() * (window.innerWidth - 100); 

    teddyPosition = {
      top: `${randomTop}px`,
      left: `${randomLeft}px`
    };
  });

  function handleClick() {
    // alert('Teddy bear clicked!');
    const shadow = document.querySelector('.shadow');

    shadow.style.opacity = '0';
    shadow.style.transition = 'opacity 5s ease';
    document.body.style.overflow = 'hidden';
 

  Swal.fire({
    title: "You Found Teddy! ",
    text: "You've just proven you have a keen eye. Now, imagine if that keen eye could help someone else.",
    icon: "success",
    confirmButtonText: 'Learn More'
  }).then(() => {
    openPopup();  
  });

  }
</script>

<svelte:window on:scroll={handleScroll} />

<div class="info">
  <button class=infoBtn class:hidden={isSmall} on:click={handleInfoClick}>? </button>
  <button class="charityBtn button-56" on:click={openPopup} class:hidden={isSmall}>❤ Donate</button>
</div>

<Popup isVisible={isPopupVisible} closePopup={closePopup} />


<div class="blob3" class:hidden={isSmall}>
  <svg viewBox="0 0 500 500" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" id="blobSvg" height="1000px">
    <path fill="#e59965">
      <animate attributeName="d"
        dur="10000ms"
        repeatCount="indefinite"
        values="
        M411,276Q358,302,374,364Q390,426,333.5,396.5Q277,367,251,363.5Q225,360,170.5,389Q116,418,93,377.5Q70,337,94.5,293.5Q119,250,83,201Q47,152,98.5,138Q150,124,173,69Q196,14,235.5,77.5Q275,141,303,145Q331,149,385,154Q439,159,451.5,204.5Q464,250,411,276Z;
      
M418.5,274.5Q352,299,366.5,357Q381,415,328,387.5Q275,360,239,408.5Q203,457,184.5,406Q166,355,107,351Q48,347,67.5,298.5Q87,250,60,197.5Q33,145,74,113Q115,81,171,115Q227,149,252.5,137.5Q278,126,299,144Q320,162,364.5,167.5Q409,173,447,211.5Q485,250,418.5,274.5Z;
M418.5,299Q454,348,394,351.5Q334,355,307,368.5Q280,382,241,420.5Q202,459,182.5,409.5Q163,360,98,357Q33,354,57,302Q81,250,70,204Q59,158,113.5,152.5Q168,147,194,132.5Q220,118,255.5,95Q291,72,307.5,115Q324,158,377,160.5Q430,163,406.5,206.5Q383,250,418.5,299Z;
M411,276Q358,302,374,364Q390,426,333.5,396.5Q277,367,251,363.5Q225,360,170.5,389Q116,418,93,377.5Q70,337,94.5,293.5Q119,250,83,201Q47,152,98.5,138Q150,124,173,69Q196,14,235.5,77.5Q275,141,303,145Q331,149,385,154Q439,159,451.5,204.5Q464,250,411,276Z"      
      >
      </animate>
    </path>
  </svg>
</div>


<div class="header" class:small={isSmall} >
  <div class="inside">
    <h1 class="header_logo" class:small={isSmall} >{headerText}</h1>
  </div>
  
  <div class="hideContent">
    <div class=game>
      
      <div class=gameText>
        <p >Glaucoma is a leading cause of irreversible vision loss. This interactive game will give you a taste of the challenges faced by people with glaucoma. 
          <span style="color:#fcd66b; font-weight:500">Can you find the hidden teddy bear? </span></p>
        <h4>Scroll down to begin your adventure and help us raise awareness for glaucoma.</h4>
        
      </div>
      
    </div>
    
    
    <svg class="arrows">
      <path class="a2" d="M0 20 L30 52 L60 20"></path>
      <path class="a3" d="M0 40 L30 72 L60 40"></path>
    </svg>
  </div>
  <div class=poster class:small={isSmall} >
    <img
    class="teddy1"
    src="teddy.png"
    alt="Teddybear"
    width="200"
    height="200"
    class:small={isSmall}
   
  >
  </div>
</div>

<div class="wrapper" class:hidden={isSmall} >
  <div class="shadow" class:hidden={!isSmall}></div>
  <div class="offset">
   
  </div >

  <div class=TeddyDiv> <img
    class="teddy"
    src="teddy.png"
    alt="Teddybear"
    width="100"
    height="100"
    style="top: {teddyPosition.top}; left: {teddyPosition.left};"
    on:click={handleClick}
    class:hidden={!isSmall}
  ></div>
 
</div>



<style>

  .game{
    display: flex;
    justify-content: center;
    gap:100px;
  }

  .gameText{
    width: 80%;
    display: flex;
    justify-content: center;
    flex-direction: column;;
    text-align: left;
  }

  .gameText>p{
    font-size: 18px;;
  }

  .poster {
  width: 200px;
  height: 200px; 
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid #e59965;
  border-radius: 50%; 
  padding: 10px;
  background-color: #f5d6c23d;
  
}

.poster.small{
  width: 10px;
  height: 10px;
  visibility: hidden;
}

.teddy1.small{
  width: 10px;
  height:10px;
  
}

.TeddyDiv{
  padding: 100px;
}

  .teddy{
    visibility:visible;
    transition: visibility 5s ease;


  }

  .teddy.hidden{
    visibility: hidden;
    transition: visibility 0s ease;

  }

  .teddy:hover{
    transform: scale(0.9);
  }
.wrapper {
  height: 120vh;
  /* background-image: url("public/img8.png"); */
  background-size: cover;
  position: relative;
  overflow: hidden;
}
.wrapper.hidden{


}

.shadow{
  position: absolute;
  width: 200vw;
  height: 200vh;
  left: 50%;
  top:50%;
  transform: translateX(-50%) translateY(-50%);
  background-image: radial-gradient(circle at center, transparent, #000 12%);
  transition: opacity 0.2s ease, transform 0.2s ease; 
  opacity: 1;
  pointer-events: none;

}

.shadow.hidden {
  opacity: 0;
  transform: translateX(-50%) translateY(-50%) scale(0.9);
}


  .header {
    position: fixed;
    top: 28%;
    left: 200px;
    right: 200px;
    background-color: #fff;
    color: #333;
    border: 2px solid #465b70;
    border-radius: 10px;
    padding: 50px 40px; 
    transition: padding 0.7s ease; 
    z-index: 10;
    transition: top 1s ease, left 1s, right 1s;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;

    display: flex;
    justify-content: center;
    align-items: center;

  }



  /* Logo styles */
  .header_logo {
    margin: 0;
    font-size: 40px;
    transition: font-size 1s ease;
    background-color: #fff;
    color: #333;
  }

  .header_logo.small {
    margin: 0;
    font-size: 32px; 
    transition: font-size 1s ease;
    border: 2px solid pink;
    padding: 20px 20px; 
    width:500px;
    background-color: #fff;
    color: #333;
    border: 2px solid #465b70;
    border-radius: 10px;
    margin:10px;
    letter-spacing: 1px;;
    border: 2px solid #fcd66b;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.35) 0px -2px 6px 0px inset;
  }

  /* Reduced size styles when scrolling */
  .header.small {
    top: 0;
    left: 0;
    right: 20;
    padding:0px;
    background-color: transparent;
    color: #333;
    border: 2px solid transparent;
    border-radius: 10px;
    width:600px;
    transition: top 1s ease, left 1s, right 1s;
    box-shadow: none;


  }

  .header.small .header_logo {
    font-size: 18px;  /* Smaller font size when scroll position is greater than 10px */
  }

  /* Initial styles for .hideContent */
  .hideContent {
    opacity: 1;
    height: auto; /* Ensures the content takes up space when visible */
    overflow: hidden; /* Prevents content from overflowing when collapsing */
    transition: opacity 0.7s ease, height 0.7s ease; /* Transition opacity and height */
  }

  /* When header is small, hide content */
  .header.small .hideContent {
    opacity: 0;
    height: 0; /* Collapses the height to 0 when hidden */
    transition: opacity 0.7s ease, height 0.7s ease; /* Smooth transition for opacity and height */
  }

  /* Offset content to ensure it doesn't get hidden by fixed header */
  .offset {
    margin-top: 100px;  /* Space to push the content below the header */
    padding: 20px;
  }

  .inside {
    display: flex;
    justify-content: space-between;
  }

  /* BLOB CSS */
  .blob {
    position: absolute;
    top: -10%;
    left: 60%;
    fill: #023F92;
    width: 50vmax;
    z-index: -1;
    animation: move 10s ease-in-out infinite;
    transform-origin: 50% 50%;
  }

  .blob2 {
    position: absolute;
    top: 5%;
    left: -10%;
    fill: #023F92;
    width: 50vmax;
    z-index: -1;
    animation: move 10s ease-in-out infinite;
    transform-origin: 50% 50%;
  }

  .blob3 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* Centers the element */
  
  fill: #023F92;
  z-index: -1;
  animation: move 10s ease-in-out infinite;
  transform-origin: -50% -50%;
}


  
.blob.hidden, .blob2.hidden, .blob3.hidden {
  visibility: hidden; 
   opacity: 0;
}

.blob, .blob2, .blob3{
  filter: drop-shadow(0.35rem 2rem 0.4rem rgba(0, 0, 0, 0.151));
  box-shadow: rgba(17, 12, 46, 0.15)

}


.blob3 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* Centers the element */
  z-index: -1;
  animation: move 10s ease-in-out infinite;
  transform-origin: center center; /* Keeps the center as the reference point */
  width: 100%; /* Make the blob fill the container width */
  height: auto; /* Maintain aspect ratio */
}

.blob, .blob2, .blob3 {
  filter: drop-shadow(0.35rem 2rem 0.4rem rgba(0, 0, 0, 0.151));
  box-shadow: rgba(17, 12, 46, 0.15);
}




.info {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 10;
  margin: 20px;
  display: flex;
  gap: 15px;
  justify-content: center;
  align-items: center;
}

.infoBtn {
  background-color: transparent;
  border: 2px solid #436062;
  border-radius: 50%; /* Makes the button circular */
  width: 28px; 
  height: 28px; 
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  font-weight: 700;;
  color: #436062; 
  cursor: pointer;
}

.infoBtn.hidden{
  border: 2px solid #7ea0a2;
  color: #7ea0a2;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  
}

.button-56 {
  align-items: center;
  background-color: #7ea0a2;
  border: 2px solid #436062;
  border-radius: 8px;
  box-sizing: border-box;
  color: #ffffff;
  cursor: pointer;
  display: flex;
  font-family: Inter, sans-serif;
  font-size: 18px;
  height: 48px;
  justify-content: center;
  line-height: 24px;
  max-width: 100%;
  padding: 0 25px;
  position: relative;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  text-transform: uppercase;
  font-weight: 500;
}


.button-56:after {
  background-color: #436062;
  border-radius: 8px;
  content: "";
  display: block;
  height: 48px;
  left: 0;
  width: 100%;
  position: absolute;
  top: -2px;
  transform: translate(8px, 8px);
  transition: transform .2s ease-out;
  z-index: -1;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.button-56.hidden {
  border: 2px solid #fff;

}
.button-56.hidden:after{
  background-color: #fff;

}

.button-56:hover:after {
  transform: translate(0, 0);
}

.button-56:active {
  background-color: #436062;
  transform: scale(0.9);
  transition: transform 0.8s ease;
  outline: 0;
}

.button-56.hidden:active {
  background-color: #436062;
  transform: scale(0.9);
  transition: transform 0.8s ease;
  outline: 0;
  color: #436062;
}


.button-56:hover {
  outline: 0;
}

@media (min-width: 768px) {
  .button-56 {
    padding: 0 40px;
  }
}


 /* @keyframes move {
  0%   { transform: scale(1)   translate(10px, -30px); }
  38%  { transform: scale(0.8, 1) translate(80vw, 30vh) rotate(160deg); }
  40%  { transform: scale(0.8, 1) translate(80vw, 30vh) rotate(160deg); }
  78%  { transform: scale(1.3) translate(0vw, 50vh) rotate(-20deg); }
  80%  { transform: scale(1.3) translate(0vw, 50vh) rotate(-20deg); }
  100% { transform: scale(1)   translate(10px, -30px); }
}  */


.arrows {
	width: 60px;
	height: 72px;
	position: absolute;
	left: 50%;
	margin-left: -30px;
	bottom: 20px;
}

.arrows path {
	stroke: #5a8689;
	fill: transparent;
	stroke-width: 3px;	
	animation: arrow 2s infinite;
	-webkit-animation: arrow 2s infinite; 
}

@keyframes arrow
{
0% {opacity:0}
40% {opacity:1}
80% {opacity:0}
100% {opacity:0}
}

@-webkit-keyframes arrow /*Safari and Chrome*/
{
0% {opacity:0}
40% {opacity:1}
80% {opacity:0}
100% {opacity:0}
}

.arrows path.a1 {
	animation-delay:-1s;
	-webkit-animation-delay:-1s; /* Safari 和 Chrome */
}

.arrows path.a2 {
	animation-delay:-0.5s;
	-webkit-animation-delay:-0.5s; /* Safari 和 Chrome */
}

.arrows path.a3 {	
	animation-delay:0s;
	-webkit-animation-delay:0s; /* Safari 和 Chrome */
}

</style>
