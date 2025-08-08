# Repositorio de prueba
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Instalación de Icarus Verilog y GTKWave en Termux</title>
  <style>
    body { font-family: Arial, sans-serif; background-color: #f4f4f4; margin: 0; padding: 0; }
    header { background-color: #333; color: white; padding: 1em; text-align: center; position: sticky; top: 0; z-index: 1000; }
    nav { background-color: #444; display: flex; justify-content: center; padding: 0.5em; flex-wrap: wrap; }
    nav a { color: white; margin: 0.5em; text-decoration: none; padding: 0.5em; border-radius: 5px; }
    nav a:hover { background-color: #666; }
    section { padding: 2em; background-color: white; margin: 1em; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    footer { background-color: #333; color: white; text-align: center; padding: 1em; }
    h1, h2 { color: white; margin: 0; }
    code { background: #eee; padding: 2px 4px; border-radius: 4px; }
    pre { background: #eee; padding: 10px; border-radius: 4px; overflow-x: auto; }
  </style>
</head>
<body>
  <header>
    <h1>🔧 Instalación de Icarus Verilog y GTKWave en Termux</h1>
  </header>
  <nav>
    <a href="#requisitos">Requisitos</a>
    <a href="#instalacion">Instalación</a>
    <a href="#verificacion">Verificación</a>
    <a href="#proyecto">Ejemplo</a>
    <a href="#errores">Errores comunes</a>
    <a href="#exportacion">Exportar archivos</a>
  </nav>

  <section id="requisitos">
    <h2>📋 Requisitos previos</h2>
    <ul>
      <li>Instalar la app <strong>Termux</strong> desde F-Droid o GitHub.</li>
      <li>Conceder permisos a almacenamiento: <code>termux-setup-storage</code></li>
    </ul>
  </section>

  <section id="instalacion">
    <h2>⚙️ Instalación de herramientas</h2>
    <pre><code>pkg update && pkg upgrade
pkg install git
pkg install clang
pkg install make
pkg install iverilog
pkg install gtkwave
pkg install nano</code></pre>
  </section>

  <section id="verificacion">
    <h2>✅ Verificación básica</h2>
    <p>Crea el siguiente archivo:</p>
    <pre><code>nano test.v</code></pre>
    <p>Contenido:</p>
    <pre><code>module main;
  initial begin
    $display("Hola desde Verilog en Termux!");
    $finish;
  end
endmodule</code></pre>
    <p>Compilar y ejecutar:</p>
    <pre><code>iverilog test.v -o test
vvp test</code></pre>
  </section>

  <section id="proyecto">
    <h2>💡 Proyecto 1: Comparador</h2>
    <p>Crea dos archivos:</p>
    <ul>
      <li><strong>comparador.v</strong>: Contiene el módulo de la Comparador</li>
      <li><strong>comparador_tb.v</strong>: Contiene el testbench</li>
    </ul>
    <p>Compilar:</p>
    <pre><code>iverilog -o sim comparador.v comparador_tb.v</code></pre>
    <p>Ejecutar:</p>
    <pre><code>vvp sim</code></pre>
    <p>Genera un archivo <code>.vcd</code> que puedes visualizar con GTKWave si deseas usar entorno gráfico.</p>
  </section>

  <section id="errores">
    <h2>🛑 Solución a errores comunes</h2>
    <ul>
      <li><strong>Error:</strong> <code>-o: No such file or directory</code><br>
        <strong>Solución:</strong> Asegúrate de que la ruta de salida del archivo esté correctamente especificada y que no estés ejecutando <code>test.v -o test</code>, lo correcto es: <code>iverilog test.v -o test</code>
      </li>
      <li><strong>Error:</strong> <code>Preprocessor failed with 1 errors.</code><br>
        <strong>Solución:</strong> Verifica si el preprocesador <code>cpp</code> está instalado. Ejecuta:
        <pre><code>pkg install clang</code></pre>
        Luego:
        <pre><code>which cpp
export IVERILOG_CPP="cpp"</code></pre>
      </li>
      <li><strong>Error:</strong> <code>Invalid module instantiation</code><br>
        <strong>Solución:</strong> Asegúrate de que estés instanciando correctamente el módulo y que los nombres coincidan entre el testbench y el archivo principal.</li>
      <li><strong>Error:</strong> <code>Unable to bind wire/reg/memory</code><br>
        <strong>Solución:</strong> Este error aparece cuando el nombre del módulo instanciado en el testbench no coincide con el nombre del módulo definido.</li>
      <li><strong>¿No se generan archivos .vcd?</strong><br>
        <strong>Solución:</strong> Verifica que hayas llamado correctamente a <code>$dumpfile("archivo.vcd");</code> y <code>$dumpvars();</code> dentro del testbench.</li>
    </ul>
  </section>

  <section id="exportacion">
    <h2>📂 Exportar archivos al almacenamiento del celular</h2>
    <p>Para copiar archivos como <code>.v</code>, <code>.vcd</code> o binarios generados (<code>sim</code>) desde Termux a una carpeta accesible del celular:</p>
    <pre><code>mkdir -p /sdcard/Download/verilog_sim
cp *.v *.vcd sim /sdcard/Download/verilog_sim/</code></pre>
    <p>Esto colocará todos los archivos útiles en la carpeta <strong>Download/verilog_sim</strong> de tu almacenamiento interno.</p>

    <h3>📦 Exportar todo en un ZIP</h3>
    <p>También puedes comprimir los archivos simulados en un solo archivo ZIP para facilitar el envío o respaldo:</p>
    <pre><code>pkg install zip
zip verilog_sim.zip *.v *.vcd sim
mv verilog_sim.zip /sdcard/Download/</code></pre>
    <p>Esto generará el archivo <code>verilog_sim.zip</code> directamente en tu carpeta de <strong>Descargas</strong>.</p>
  </section>

  <footer>
    <p>Hecho con ❤️ para usuarios de Verilog en Android</p>
  </footer>
</body>
</html>
