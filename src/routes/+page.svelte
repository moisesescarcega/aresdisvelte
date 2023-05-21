<script>
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';

  // Datos del sitio web
  let logoRotation = 0;
  let phrases = ['Diseño arquitectónico', 'Planos y dibujo técnico', 'Renders'];
  let currentPhrase = phrases[0];
  let visible = false;
  $: rota = logoRotation + 'deg';
    
  // Función para rotar el logo
  function rotateLogo() {
      logoRotation += 120;
  }

  // Función para cambiar la frase
  function changePhrase() {
    const currentIndex = phrases.indexOf(currentPhrase);
    const nextIndex = (currentIndex + 1) % phrases.length;
    currentPhrase = phrases[nextIndex];
  }

  function aparece() {
    setTimeout(()=> { visible = false; },2500);
    setTimeout(()=> { visible = true; },500);
  };

  // Llamar a las funciones de forma recurrente
  onMount(() => {
      visible = true;
      setTimeout(()=> { visible = false; }, 2500);
      setInterval(aparece, 3000);
      setInterval(changePhrase, 3000); // Cambiar la frase cada 3 segundos
      setInterval(rotateLogo, 3000); // Rotar el logo cada 3 segundos
  });
</script>

<svelte:head>
  <title>aresdi</title>
</svelte:head>

<div class="row color-change-3x">
  <div class="column color-change-3x shadow-change-3x">

    <img src="logo_aresdi_pt.png" style="transform:rotate({rota})" alt="Logo Aresdi" class="logo" id="logo">

    <div class="logo-text">aresdi</div>
    <div class="subtexto">arquitectura espacio diseño</div>
    <div class="mailto">
      <a href="mailto:contacto@aresdi.com">contacto@aresdi.com</a>
    </div>
    <a aria-label="Chat on WhatsApp" href="https://wa.me/525517742133?text=Hola%20aresdi,%20quisiera%20ayuda%20con%20mi%20proyecto%20de%20">
      <img alt="Chat on WhatsApp" class="chatwa" src="WhatsAppButtonWhiteSmall.png" />
    </a>
    <p class="subtexto">San Miguel de Allende, <br />Gto. México</p>
  </div>
  <div class="column2 color-change-3x">
    {#if visible}
    <p class="phrase" id="phrase" transition:fade>{currentPhrase}</p>
    {/if}
  </div>
</div>
