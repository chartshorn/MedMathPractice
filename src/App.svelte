<script>
  import AppButton from './lib/Button.svelte'
  import MedicationCard from './lib/MedicationCard.svelte'

  //global (config) vars
  const minAdultWeight = 40; // min weight (kilos)
  const maxAdultWeight = 130; // max weight (kilos)
  const minAdultAge = 18; // min adult age (years)
  const maxAdultAge = 99; // max adult age (years)

  //function delcaration
  //generates a random number between the min and max
  function getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
  }
  
  //var declaration
  const currentMed = {
    name: "Dopamine", // name of med
    doseOnHand: 400, // dose in mg
    volume: 250, // volume in mL
    adminReason: "Hypotension", // reason why you are administering
    dose: "5mcg/kg/min", // dose ordered
    route: "IVPB (Infusion)", // route to give med
    type: "INFUSION"
  }

  const ptInfo = {
    gender: "", // gender m/f
    age: 0,
    weight: 0 // weight in lbs
  }
  
  //map inputs -> outputs
  const generateNewScenario = () => {
    //generate pt info
    //generate pt gender & age
    ptInfo.gender = Math.random() < 0.5 ? "M" : "F";
    ptInfo.age = getRandomInt(minAdultAge, maxAdultAge);
    //generate pt weight
    ptInfo.weightKg = getRandomInt(minAdultWeight, maxAdultWeight);
    ptInfo.weight = Math.round(ptInfo.weightKg *2.2);
  }

  generateNewScenario();
</script>

<main>
  <h1>Med Math Practice</h1>

  <p>You have a {ptInfo.weight} pound {ptInfo.age} y/o {ptInfo.gender}, presenting with { currentMed.adminReason }. Via online medical direction, you have been ordered to administer { currentMed.dose } of { currentMed.name } via { currentMed.route }. Below is the package your medication comes in. </p>
  <hr />

  <div class="medication-area">
    <MedicationCard medication={currentMed} />
    <MedicationCard medication={currentMed} />
  </div>
  
  <AppButton on:click={generateNewScenario}/>
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
