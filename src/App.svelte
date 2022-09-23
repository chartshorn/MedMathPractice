<script>
  import AppButton from './lib/Button.svelte'
  import MedicationArea from './lib/MedicationArea.svelte'

  //var declaration
  const currentMed = {
    name: "Dopamine",
    doseOnHand: 400, // dose in mg
    volume: 250, // volume in mL
    adminReason: "Hypotension",
    dose: "5mcg/kg/min",
    route: "IVPB (Infusion)"
  }

  const ptInfo = {
    gender: "M", // gender m/f
    weight: "176" // weight in lbs
  }
  
  //map inputs -> outputs
  const generateNewScenario = () => {
    console.log("hello world!");
  }

  generateNewScenario();
</script>

<main>
  <h1>Med Math Practice</h1>

  <p>You have a {ptInfo.weight} pound {ptInfo.gender}, presenting with { currentMed.adminReason }. Via online medical direction, you have been ordered to administer { currentMed.dose } of { currentMed.name } via { currentMed.route }. Below is the package your medication comes in. </p>
  <hr />
  <h2>{ currentMed.name }</h2>
  <p>
    Dose On Hand: { currentMed.doseOnHand }, <br />
    Volume: { currentMed.volume } <br />
  </p>
  
  
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
</style>
