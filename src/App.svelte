<script>
  import AppButton from './lib/Button.svelte'
  import MedicationCard from './lib/MedicationCard.svelte'
  import Spoiler from './lib/Spoiler.svelte'
  import data from './data/data.json'

  //global (config) vars
  const minAdultWeight = 40; // min weight (kilos)
  const maxAdultWeight = 130; // max weight (kilos)
  const minAdultAge = 18; // min adult age (years)
  const maxAdultAge = 99; // max adult age (years)
  const medList = data.meds;

  //function delcaration
  //generates a random number between the min and max
  function getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
  }

  //search array for a specific med
  //arguments - string medName - name of medication to search for
  //returns - object Medication
  function searchDataForMed(medName) {
    for (let i = 0; i < medList.length; i++) {
      if (medList[i].name === medName) {
        return medList[i];
      }
    }
  }

  //calculate infusion
  function calculateInfusionDose(medication) {
    let dose = medication.dose;
    if (medication.doseSuffix.search("mcg") >= 0) {
      dose *= 0.001;
    }
    if (medication.doseSuffix.search("kg") >= 0) {
      dose *= ptInfo.weightKg;
    }
    //infusion formula (dose per min * dripset) / dose on hand
    currentMed.calculatedGtt = Math.round((dose * medication.dripset) / (medication.doseOnHand / medication.volume))
  }
  
  //var declaration
  let userGtt = 0;
  let userResult = "";
  
  let currentMed = {
    name: "NAME", // name of med
    doseOnHand: 0, // dose in mg
    volume: 0, // volume in mL
    adminReason: "ADMINREASON", // reason why you are administering
    dose: "DOSE", // dose ordered
    doseSuffix: "DOSESUFFIX",
    doseMin: 0,
    doseMax: 0,
    route: "ROUTE", // route to give med
    type: "TYPE", // Infusion, IVP, ETC
    order: "ORDER", // is med standing order or require BHO
    dripset: "DRIPSET",
    calculatedGtt: 0
  }

  const ptInfo = {
    gender: "", // gender m/f
    age: 0, // age in years
    weight: 0, // weight in lbs
    weightKg: 0 // weight in kgs
  }
  
  //map inputs -> outputs
  const generateNewScenario = () => {
    //var init
    let randomMedIndex; // index of random med in medication list
    let randomDose; // generated random dose of med
    
    //generate pt info
    //generate pt gender & age
    ptInfo.gender = Math.random() < 0.5 ? "M" : "F";
    ptInfo.age = getRandomInt(minAdultAge, maxAdultAge);
    //generate pt weight
    ptInfo.weightKg = getRandomInt(minAdultWeight, maxAdultWeight);
    ptInfo.weight = Math.round(ptInfo.weightKg *2.2);
    //create new random med
    randomMedIndex = getRandomInt(0, medList.length-1);
    currentMed = { ... medList[randomMedIndex] };

    //generate dose
    randomDose = getRandomInt(currentMed.doseMin, currentMed.doseMax);
    currentMed.dose = randomDose;
    //calculate infusion dose
    calculateInfusionDose(currentMed);
    //reset user feedback
    userResult = "-";
  }

  const gradeGuess = () => {
    const indexOfError = currentMed.calculatedGtt - userGtt;
    let tempString = ""; 
    if (indexOfError >= -1 && indexOfError <= 1) {
      tempString = "Correct.";
    } else {
      tempString = "Potentially incorrect."
    }
    tempString += " System calculated dose as " + currentMed.calculatedGtt + " gtts/min";
    userResult = tempString;
  }

  //init scenario
  generateNewScenario();
</script>

<main>
  <h1>Med Math Practice</h1>

  <p>You have a {ptInfo.weight} pound (<Spoiler>{ptInfo.weightKg}</Spoiler>kg) {ptInfo.age} y/o {ptInfo.gender}, presenting with { currentMed.adminReason }. Via {currentMed.order}, you have been ordered to administer { currentMed.dose }{ currentMed.doseSuffix } of { currentMed.name } via { currentMed.route }. Below is the package your medication comes in. You have a {currentMed.dripset} gtt/min dripset available. How many drips per minute should you deliver? </p>
  <hr />

  <div class="medication-area">
    <MedicationCard medication={currentMed} />
  </div>
  <hr />
  <p>{userResult}</p>
  <input type="text" bind:value={userGtt}>
  <AppButton on:click={gradeGuess}>Check Dose</AppButton>
  <AppButton on:click={generateNewScenario}>New Scenario</AppButton>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  h2 {
    padding-bottom: 0;
    line-height: 0;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }

  .medication-area {
    display: flex;
    margin: 25px -15px;
  }
</style>
