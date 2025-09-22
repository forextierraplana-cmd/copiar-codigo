<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Copiar código del producto</title>
<style>
  body{
    font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial;
    margin:0;
    padding:2rem;
    background:#f6f7fb;
    color:#111;
  }
  .card{
    max-width:520px;
    margin:2rem auto;
    background:#fff;
    padding:1.4rem;
    border-radius:12px;
    box-shadow:0 8px 24px rgba(10,10,10,.06);
    text-align:center;
  }
  .codeBox{
    font-size:1.5rem;
    padding:.75rem 1rem;
    border:1px dashed #ddd;
    border-radius:8px;
    display:inline-block;
    user-select:text;
    cursor:pointer;
  }
  button{
    margin-top:1rem;
    padding:.6rem 1rem;
    border:0;
    border-radius:8px;
    cursor:pointer;
    font-size:1rem;
    background:#0b84ff;
    color:#fff;
  }
  small{
    display:block;
    margin-top:.7rem;
    color:#666;
  }
</style>
</head>
<body>
  <div class="card">
    <h2>Copiar código del producto</h2>
    <div id="code" class="codeBox" onclick="selectText()" aria-readonly="true">ABC12345</div>
    <br>
    <button id="copyBtn">Copiar código</button>
    <small>Toca el código o usa el botón para copiar. Luego pegalo en el buscador de mercado libre.</small>
  </div>

<script>
  // Función para leer el parámetro ?code=
  function getParam(name){
    try{ 
      const url = new URL(location.href);
      return url.searchParams.get(name); 
    }catch(e){return null;}
  }

  const codeStr = getParam('code') ? decodeURIComponent(getParam('code')) : 'ABC12345';
  const codeEl = document.getElementById('code');
  codeEl.textContent = codeStr;

  function selectText(){
    if(window.getSelection && document.createRange){
      const range = document.createRange();
      range.selectNodeContents(codeEl);
      const sel = window.getSelection();
      sel.removeAllRanges();
      sel.addRange(range);
    }
  }

  document.getElementById('copyBtn').addEventListener('click', async () => {
    try{
      await navigator.clipboard.writeText(codeStr);
      alert('Código copiado: ' + codeStr);
    }catch(e){
      // fallback si el navegador no soporta navigator.clipboard
      selectText();
      document.execCommand('copy');
      alert('Código copiado (método alterno)');
    }
  });
</script>
</body>
</html>
