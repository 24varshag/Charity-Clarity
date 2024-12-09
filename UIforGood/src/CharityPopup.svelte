<script>
    export let isVisible = false;
    export let closePopup = () => {};
    import Swal from 'sweetalert2'

    
    // Set default values for selected donation type and amount
    let donationType = "One Time";
    let donationAmount = 1;
  
    // Store the formatted donation string
    let donationString = `Donation of $${donationAmount.toFixed(2)} ${donationType}`;
    
    // Function to handle button click and update donation selection
    function selectDonationType(type) {
      donationType = type;
      donationString = `Donation of $${donationAmount.toFixed(2)} ${donationType}`;
    }
  
    function selectAmount(amount) {
      donationAmount = amount;
      donationString = `Donation of $${donationAmount.toFixed(2)} ${donationType}`;
    }

  function handleInputAmount(event) {
    donationAmount = parseFloat(event.target.value) || 0; // Ensure it's a valid number
    donationString = `Donation of $${donationAmount.toFixed(2)} ${donationType}`;
  }

  function showDonationAlert() {
    Swal.fire({
  icon: "success",  
  title: "Thank You For Your Gift",
  text: donationString,  
  footer: '<a href="https://www.mayoclinic.org/diseases-conditions/glaucoma/symptoms-causes/syc-20372839">Learn More About Glaucoma</a>'
});
  }
  </script>
  
  {#if isVisible}
   
    <div class="popup-overlay" on:click={closePopup}>
      <div class="popup-content" on:click|stopPropagation>
        <div class="leftSide">
          <div id='show_bg_2'>
            <div><h1>Glaucoma: The Silent Thief of Sight</h1>
              <p style="font-size: 18px;">Glaucoma is a serious eye condition that can lead to irreversible vision loss. It often develops slowly and painlessly, making early detection crucial.</p>
            </div>
          </div>
          <div class="causeInfo">
            <h2 style="color: #5b6468;">Why Donate?</h2>
            <div class="infobox-container">
                <div class="infobox" style="background-color:#feedbf; text">
                    <h4> <a href="https://www.glaucoma.org/donate">Support Research</a> </h4>
                    <p>Your donation helps fund research for a glaucoma cure, new treatments, and better patient outcomes.</p>

                  </div>
                  <div class="infobox" style="background-color:#e5e1e0;">
                    <h4><a href="https://www.americanglaucomasociety.net/donate">Promote Early Detection</a></h4>
                    <p>Your support funds screening programs to identify high-risk individuals and prevent vision loss.</p>
                  </div>
                  <div class="infobox" style="background-color:#f5d6c2;">
                    <h4><a href="https://www.brightfocus.org/glaucoma">Offer Essential Support</a></h4>
                    <p>Your generosity provides resources like low-vision aids, support groups, and counseling for patients and families.</p>
                  </div>
                  
            </div>
          </div>

        </div>
  
        <div class="rightSide">
          <h1 class="donation">Donation</h1>
  
          <p class="dp" style="text-align:left;margin-bottom:10px; font-size:16px; font-weight:500;">Please make my donation</p>
  
          <div class="time">
            <button 
              class="button1" 
              class:selected={donationType === 'One Time'} 
              on:click={() => selectDonationType('One Time')}
            >
              One Time
            </button>
            <button 
              class="button1" 
              class:selected={donationType === 'Monthly'} 
              on:click={() => selectDonationType('Monthly')}
            >
              Monthly
            </button>
          </div>
  
          <p class="dp" style="text-align:left; font-size:16px; font-weight:500;">I would like to donate</p>
  
          <div class="money">
            <button 
              class="button2" 
              class:selected={donationAmount === 1} 
              on:click={() => selectAmount(1)}
            >
              $1
            </button>
            <button 
              class="button2" 
              class:selected={donationAmount === 5} 
              on:click={() => selectAmount(5)}
            >
              $5
            </button>
            <button 
              class="button2" 
              class:selected={donationAmount === 10} 
              on:click={() => selectAmount(10)}
            >
              $10
            </button>
            <button 
              class="button2" 
              class:selected={donationAmount === 25} 
              on:click={() => selectAmount(25)}
            >
              $25
            </button>
            <button 
              class="button2" 
              class:selected={donationAmount === 50} 
              on:click={() => selectAmount(50)}
            >
              $50
            </button>
            <button 
              class="button2" 
              class:selected={donationAmount === 100} 
              on:click={() => selectAmount(100)}
            >
              $100
            </button>
          </div>
  
          <p style="margin-left:20px;margin-bottom:0px;font-size:16px; font-weight:500;">OR</p>
  
          <div>
            <span class="currencyinput">$<input type="text" name="currency" placeholder="1000" on:input={handleInputAmount} value={donationAmount}></span>
        </div>
  
          <button class="button-27" on:click={showDonationAlert}>Donate</button>
        </div>

      </div>
    </div>
  {/if}
  <style>

@import url('https://fonts.googleapis.com/css2?family=Playwrite+GB+S:ital,wght@0,100..400;1,100..400&family=Roboto+Mono:ital,wght@0,100..700;1,100..700&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&family=Tangerine:wght@400;700&display=swap');
a {
  text-decoration: none; 
  color: inherit;         
}
h4 {
  text-decoration: underline;
}
.selected {
    border: 2px solid #3498db; 
  }

  .button1, .button2 {
    padding: 10px 20px;
    margin: 5px;
    border: 0;
    cursor: pointer;
  }

  .button1.selected, .button2.selected {
    border: 0; 
    box-shadow: inset 0 0 0 2px #3371e6;  }





#show_bg_2 {
    background-image: linear-gradient(to bottom, rgba(245, 246, 252, 0.52), rgba(117, 19, 93, 0.856)),
        url("public/eye.png");
    width: calc(100% - 20px);
    height: 300px; 
    background-size: cover;
    background-position: center; 
    color: white;
    display: flex;
    justify-content: center;
    text-align: left;
    padding-left: 20px;
    padding-top: 20px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    border-bottom: 2px solid black;
    position: relative;
    flex-shrink: 0; 
}

#show_bg_2 div {
    position: absolute;
    bottom: 10px; 
    left: 20px;  
}

#show_bg_2 div>h1{
    margin-bottom:0px;
    padding-bottom:0px;
}


.causeInfo{
    margin: 20px;
    margin-top:0px;
}

.infobox-container {
  display: flex;
}




.infobox {
  border-radius: 10px;
  text-align: left;
  transition: transform 0.3s ease;
  margin:0px 7px;
  padding:10px;
}

.infobox>p {
    font-size: 0.9rem;
    color: #6b6b82;
  }

  .togo{
    /* font-family: "Tangerine"; */
    font-size: 30px;
    text-align: center;
    margin:0px;
    margin-top:20px;
  }

    .popup-overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
  
    .popup-content {
      padding: 20px;
      border-radius: 10px;
      width: 80%;
      height: 80%;
      text-align: center;

      display: flex;
      flex-direction: row;
      padding:20px;
      justify-content: center;
    }

    .leftSide, .rightSide{
        /* border: 2px solid black; */
        margin:5px;
        border-radius: 10px;;
        background-color: #fff;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);

    }

    .leftSide{
        width:65%;
        display: flex;
        flex-direction: column;
        text-align: left;
    }

    .rightSide{
        width:30%;
        padding:20px;
    }

  
   .button1{
    align-items: center;
    text-align: center;
    border-radius: 8px;
    font-size: 16px;
    padding: 15px 30px;
    border: 2px solid #ccc;
    background-color: #fff;
    width: 100%;
    cursor: pointer;

   }

   .button1:hover{
    background: #ebf1fc;
    box-shadow: inset 0 0 0 2px #3371e6;

   }

   .time{
    display: flex;
    justify-content: space-evenly;
    margin: 0px;

   }

   .money {
    margin: 0px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    gap: 10px; 
}

.button2 {
    border: 2px solid #ccc;
    background-color: #fff;
    padding: 15px 35px;
    border-radius: 8px;
    font-size: 16px;
    flex: 1; 
    max-width: 120px;
    text-align: center; 
    cursor: pointer;
}

.button2:hover{
    background: #ebf1fc;
    box-shadow: inset 0 0 0 2px #3371e6;

}


.currencyinput {
    border: 2px solid #ccc;
    padding: 15px 30px;
    border-radius: 8px;
    background-color: #fcd66b;
   
}
.currencyinput input {
    padding: 16px 5px;
    margin:20px;
    border:0;
    font-size: 16px;
    border-top: 2px solid #ccc;
    border-bottom: 2px solid #ccc;
    color: black;
}

.dp{
}

/* CSS */
.button-27 {
  appearance: none;
  background-color: #7ea0a2;
  border: 2px solid #436062;
  border-radius: 15px;
  color: #FFFFFF;
  cursor: pointer;
  display: inline-block;
  font-size: 18px;
  font-weight: 600;
  min-height: 60px;
  min-width: 0;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  width: 100%;
  will-change: transform;
  margin: 20px 0px;
}

.button-27:disabled {
  pointer-events: none;
}

.button-27:hover {
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

.button-27:active {
  box-shadow: none;
  transform: translateY(0);
}



  </style>
  