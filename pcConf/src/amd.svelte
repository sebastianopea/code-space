<script>

  import { navigate } from "svelte-routing";
  import { onMount } from "svelte";
  
  function goToCartPage(){
      saveConfiguration();
      navigate("/cart");
  }
  
  function goToHomePage(){
    saveConfiguration();
    navigate("/");
  }

  function saveConfiguration(){
    const configurationToSave = {
      selectedProcessor,
      selectedMotherboard,
      selectedGraphicsCard,
      selectedPowerSupply,
      selectedRam,
      selectedStorage,
      selectedCase
    };
    localStorage.setItem("pcConfigurationAMD", JSON.stringify(configurationToSave));
  }
  
    let processors = [
      { name: 'AMD Ryzen 5', price: 200 },
      { name: 'AMD Ryzen 7', price: 300 },
      { name: 'AMD Ryzen 9', price: 400 }
    ];
  
    let motherboards = {
      'AMD Ryzen 5': [
        { name: 'Scheda madre A', price: 100 },
        { name: 'Scheda madre B', price: 120 }
      ],
      'AMD Ryzen 7': [
        { name: 'Scheda madre C', price: 150 },
        { name: 'Scheda madre D', price: 180 }
      ],
      'AMD Ryzen 9': [
        { name: 'Scheda madre E', price: 200 },
        { name: 'Scheda madre F', price: 220 }
      ]
    };
  
    let graphicsCards = [
      { name: 'NVIDIA GTX 1660', price: 250 },
      { name: 'NVIDIA RTX 3060', price: 400 },
      { name: 'AMD RX 5700', price: 350 }
    ];
  
    let powerSupplies = [
      { name: '500W', price: 50 },
      { name: '600W', price: 70 },
      { name: '750W', price: 90 }
    ];
  
    let ramOptions = [
      { name: '8GB', price: 80 },
      { name: '16GB', price: 120 },
      { name: '32GB', price: 200 }
    ];
  
    let storageOptions = [
      { name: 'SSD 256GB', price: 100 },
      { name: 'SSD 512GB', price: 150 },
      { name: 'HDD 1TB', price: 80 }
    ];
  
    let cases = [
      { name: 'Case 1', price: 60 },
      { name: 'Case 2', price: 80 },
      { name: 'Case 3', price: 100 }
    ];
  
    let selectedProcessor = { name: '', price: 0 };
    let selectedMotherboard = { name: '', price: 0 };
    let selectedGraphicsCard = { name: '', price: 0 };
    let selectedPowerSupply = { name: '', price: 0 };
    let selectedRam = { name: '', price: 0 };
    let selectedStorage = { name: '', price: 0 };
    let selectedCase = { name: '', price: 0 };

    onMount(() => {
    const savedConfiguration = JSON.parse(localStorage.getItem("pcConfigurationAMD")) || {};
    selectedProcessor = savedConfiguration.selectedProcessor || { name: '', price: 0 };
    selectedMotherboard = savedConfiguration.selectedMotherboard || { name: '', price: 0 };
    selectedGraphicsCard = savedConfiguration.selectedGraphicsCard || { name: '', price: 0 };
    selectedPowerSupply = savedConfiguration.selectedPowerSupply || { name: '', price: 0 };
    selectedRam = savedConfiguration.selectedRam || { name: '', price: 0 };
    selectedStorage = savedConfiguration.selectedStorage || { name: '', price: 0 };
    selectedCase = savedConfiguration.selectedCase || { name: '', price: 0 };
  });

    $: total = calculateTotal(selectedProcessor, selectedMotherboard, selectedGraphicsCard, selectedPowerSupply,selectedRam, selectedStorage, selectedCase);
  
    function findPrice(component, componentArray, processorName) {
  if (processorName && component.name) {
    const motherboardsForProcessor = motherboards[processorName];
    if (motherboardsForProcessor) {
      const motherboard = motherboardsForProcessor.find(m => m.name === component.name);
      if (motherboard) {
        return motherboard.price;
      }
    }
  }
  const foundComponent = componentArray.find(c => c.name === component.name);
  return foundComponent ? foundComponent.price : 0;
}

function calculateTotal(selectedProcessor, selectedMotherboard, selectedGraphicsCard, selectedPowerSupply, selectedRam, selectedStorage, selectedCase) {
  total = 0;
  total += findPrice(selectedProcessor, processors);
  total += findPrice(selectedMotherboard, [], selectedProcessor.name);
  total += findPrice(selectedGraphicsCard, graphicsCards);
  total += findPrice(selectedPowerSupply, powerSupplies);
  total += findPrice(selectedRam, ramOptions);
  total += findPrice(selectedStorage, storageOptions);
  total += findPrice(selectedCase, cases);
  return total;
}
  </script>
  
  <main>
    <h1>Configurazione PC</h1>
  
    <label>
      Processore:
      <select bind:value={selectedProcessor.name}>
        {#each processors as processor}
          {#if selectedProcessor.name == processor.name}
            <option value={processor.name} selected>{processor.name} - €{processor.price}</option>
          {:else}
            <option value={processor.name} >{processor.name} - €{processor.price}</option>
          {/if}
        {/each}
      </select>
    </label>
  
    {#if selectedProcessor.name}
      <label>
        Scheda madre:
        <select bind:value={selectedMotherboard.name}>
          {#each motherboards[selectedProcessor.name] as motherboard}
          {#if selectedMotherboard.name == motherboard.name}
            <option value={motherboard.name} selected>{motherboard.name} - €{motherboard.price}</option>
          {:else}
            <option value={motherboard.name}>{motherboard.name} - €{motherboard.price}</option>
          {/if}
          {/each}
        </select>
      </label>
    {/if}
  
    <label>
      Scheda video:
      <select bind:value={selectedGraphicsCard.name}>
        {#each graphicsCards as graphicsCard}
        {#if selectedGraphicsCard.name == graphicsCard.name}
        <option value={graphicsCard.name} selected>{graphicsCard.name} - €{graphicsCard.price}</option>
        {:else}
          <option value={graphicsCard.name}>{graphicsCard.name} - €{graphicsCard.price}</option>
        {/if}
        {/each}
      </select>
    </label>
  
    <label>
      Alimentatore:
      <select bind:value={selectedPowerSupply.name}>
        {#each powerSupplies as powerSupply}
        {#if selectedPowerSupply.name == powerSupply.name}
          <option value={powerSupply.name} selected>{powerSupply.name} - €{powerSupply.price}</option>
        {:else}
          <option value={powerSupply.name} >{powerSupply.name} - €{powerSupply.price}</option>
        {/if}
        {/each}
      </select>
    </label>
  
    <label>
      RAM:
      <select bind:value={selectedRam.name}>
        {#each ramOptions as ramOption}
        {#if selectedRam.name == ramOptions.name}
          <option value={ramOption.name} selected>{ramOption.name} - €{ramOption.price}</option>
        {:else}
          <option value={ramOption.name}>{ramOption.name} - €{ramOption.price}</option>
        {/if}
        {/each}
      </select>
    </label>
  
    <label>
      Memoria di massa:
      <select bind:value={selectedStorage.name}>
        {#each storageOptions as storageOption}
        {#if storageOption.name == selectedStorage.name}
          <option value={storageOption.name} selected>{storageOption.name} - €{storageOption.price}</option>
        {:else}
          <option value={storageOption.name}>{storageOption.name} - €{storageOption.price}</option>
        {/if}
        {/each}
      </select>
    </label>
  
    <label>
      Case:
      <select bind:value={selectedCase.name}>
        {#each cases as pcCase}
        {#if pcCase.name == selectedCase.name}
          <option value={pcCase.name} selected>{pcCase.name} - €{pcCase.price}</option>
        {:else}
          <option value={pcCase.name}>{pcCase.name} - €{pcCase.price}</option>
        {/if}
        {/each}
      </select>
    </label>
  
    <section>
      <h2>Configurazione Selezionata</h2>
      <p>Processore: {selectedProcessor.name}</p>
      {#if selectedMotherboard.name}
        <p>Scheda madre: {selectedMotherboard.name}</p>
      {/if}
      <p>Scheda video: {selectedGraphicsCard.name}</p>
      <p>Alimentatore: {selectedPowerSupply.name}</p>
      <p>RAM: {selectedRam.name}</p>
      <p>Memoria di massa: {selectedStorage.name}</p>
      <p>Case: {selectedCase.name}</p>
      <p><strong>Totale: €{total}</strong></p>
    </section>
  
    <button on:click={goToCartPage}>Carello</button>
    <button on:click={goToHomePage}>Homepage</button>
  </main>
  
  <style>
    main {
      max-width: 600px;
      margin: auto;
    }
  
    label {
      display: block;
      margin-bottom: 10px;
    }
  
    section {
      margin-top: 20px;
    }
  </style>
  