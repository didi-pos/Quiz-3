<div align="center">
<h1>Quiz 3</h1>
  <p>
    Ingeniería Electrónica · Universidad Santo Tomás
    <br>
    <b>Didier Posse</b>
    <br>
    <em>Primer punto</em>
  </p>
</div>

<hr>

<div align="center">
  <h2>Dockerización Enviroment E1</h2>
</div>

<ol>
  <li><br>
    <div align="center">
      <p><img width=850 src="https://github.com/user-attachments/assets/57df6792-e978-4a4e-8ecb-11bfa736751b"/></p>
      <p><img width=850 src="https://github.com/user-attachments/assets/93a3450b-6d07-472e-bd08-4d963e448ef2"/></p>
    </div>
    <p>
      Primero se debe crear la carpeta que contendrá todos los archivos necesarios para dockerizar la simulación. Una vez creada, se ingresa a la carpeta y se crea otra llamada <b>"results"</b>, la cual almacenará los datos obtenidos de la simulación.  
      Luego, se crea el archivo <b>"Dockerfile"</b>, que contiene los comandos que indican todo lo que debe hacerse dentro del contenedor para descargar las dependencias y el repositorio que incluye los recursos necesarios para ejecutar la simulación, además de configurar el entorno de trabajo y las herramientas requeridas.
      <br><br>
      Después de eso, se usa el comando <code>xhost +local:docker</code> para permitir las conexiones X11, que son necesarias para mostrar el entorno gráfico al ejecutar el contenedor.  
      Finalmente, se construye la imagen con:  
      <code>docker build -t &lt;nombre_de_la_imagen&gt; .</code>  
      Este proceso puede tardar varios minutos, y al finalizar debe aparecer el mensaje <b>"FINISHED"</b>.
    </p>
  </li>

  <li><br>
    <div align="center">
      <p><img width=850 src="https://github.com/user-attachments/assets/1e646a3b-9cfc-4cce-8fb5-1fc908acc59a"/></p>
    </div>
    <p>
      En el archivo <b>Dockerfile</b>, cada línea cumple una función específica:
      <ul>
        <li><code>FROM ubuntu:22.04</code> → Define la imagen base del contenedor. En este caso, se usa <b>Ubuntu 22.04</b>, una versión estable y compatible con librerías gráficas y científicas necesarias para PyBullet.</li>
        <li><code>ENV DEBIAN_FRONTEND=noninteractive</code> → Configura el entorno para que las instalaciones se ejecuten sin pedir confirmaciones, lo que permite automatizar todo el proceso dentro de Docker.</li>
        <li><code>RUN apt-get update ...</code> → Actualiza los repositorios e instala los paquetes esenciales como <b>python3-pip</b>, <b>git</b>, <b>libgl1-mesa-glx</b> y <b>mesa-utils</b>. Estos paquetes permiten manejar librerías de Python, clonar repositorios y habilitar soporte gráfico (OpenGL) para la simulación. Al final, limpia la caché de <b>apt</b> para reducir el tamaño de la imagen.</li>
        <li><code>WORKDIR /app</code> → Define la carpeta de trabajo dentro del contenedor, donde se ejecutarán los comandos y se almacenará el código del proyecto.</li>
        <li><code>RUN git clone ...</code> → Clona el repositorio <b>PyBullet_Industrial_Robotics_Gym</b> directamente en la carpeta de trabajo, trayendo todo el contenido del proyecto al contenedor.</li>
        <li><code>RUN pip3 install ...</code> → Instala las librerías necesarias como <b>PyBullet</b>, <b>NumPy</b>, <b>Pandas</b>, <b>Matplotlib</b>, <b>SciPy</b>, <b>Torch</b>, <b>Stable-Baselines3</b> y <b>Gymnasium</b>. Estas permiten realizar simulaciones físicas, cálculos matemáticos, aprendizaje por refuerzo y visualización de datos.</li>
        <li><code>ENV PYTHONPATH=...</code> → Agrega la carpeta del proyecto al <b>PYTHONPATH</b> para que los módulos y scripts puedan importarse correctamente desde cualquier parte del código.</li>
        <li><code>CMD ["python3", ...]</code> → Indica el comando que se ejecutará automáticamente al iniciar el contenedor. En este caso, se lanza el script principal del entorno de simulación (<b>test_env.py</b>), que ejecuta la prueba del entorno PyBullet.</li>
      </ul>
    </p>
  </li>

  <li><br>
    <div align="center">
      <p><img width=850 src="https://github.com/user-attachments/assets/c9b149dd-6dc4-4f07-b851-c73403df8ffb"/></p>
    </div>
    <p>
      En esta imagen se muestra la ejecución del contenedor con el comando:
      <code>docker run -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --device /dev/dri &lt;nombre_de_la_imagen&gt;</code>  
      Esto permite correr la simulación dentro de Docker, pero mostrando la interfaz gráfica igual que si se ejecutara directamente en el sistema.  
      Aquí solo se muestra la ejecución de la simulación en la consola, donde se indican los datos que se pueden obtener, así como la información sobre mutex y semáforos durante la ejecución o finalización del proceso.
    </p>
  </li>

  <li><br>
    <div align="center">
      <p><img width=850 src="https://github.com/user-attachments/assets/fb616716-6391-4997-b191-6cb44db54950"/></p>
    </div>
    <p>
      Aquí ya se evidencia la simulación corriendo desde Docker como un contenedor; así se confirma que efectivamente se dockerizó el archivo y que la interfaz gráfica, específicamente la de PyBullet, se muestra correctamente.
    </p>
  </li>
</ol>

<hr>

<div align="center">
  <p><em>Segundo Punto</em></p>
</div>

<hr>

<div align="center">
  <h2>Vigilancia Tecnológica</h2>
</div>

<h2>Quantum, Biological, Computer Vision and Neural Network Systems for the Industrial Internet of Things</h2>
<p>
  <b>Patente:</b> JP2024519533A<br>
  <b>Año:</b> 2024<br>
  <b>Entidad:</b> Varian Medical Systems Inc.<br><br>
  La patente usa procesamiento de datos sensoriales y renderizado visual de gemelos digitales, lo que encaja con los trabajos de <b>visión artificial</b> y análisis de imágenes que hemos visto. También involucra <b>IoT</b> y <b>redes</b> porque usa sensores distribuidos que requieren comunicación mediante routers, switches y tecnologías como 5G o Wi-Fi.
  El procesamiento pesado puede implementarse en <b>máquinas virtuales</b> o <b>contenedores Docker</b>, igual que en los laboratorios, para escalar y aislar servicios. Además, su gestión remota y el uso de blockchain la conectan con la <b>ciberseguridad</b> aplicada a sistemas distribuidos.
  Finalmente, los nodos sensoriales y la necesidad de respuesta inmediata la vinculan con los <b>sistemas embebidos</b> y la <b>visión en tiempo real</b> que también hemos trabajado.
</p>

<h2>5G-WiFi Inside Secure Iris Biometrics’ Login</h2>
<p>
  <b>Patente:</b> US20220272084A1<br>
  <b>Año:</b> 2022<br>
  <b>Entidad:</b> Lenworth Alexander Hyatt<br><br>
  Esta patente presenta un sistema de autenticación biométrica mediante el iris, que se conecta por 5G o WiFi para validar identidades de manera remota. Usa inteligencia artificial para reconocer patrones del iris y sustituir contraseñas tradicionales.  
  En el contexto de <b>ciberseguridad</b> y <b>redes</b>, aplica directamente a lo que estamos viendo en clase: autenticación segura, comunicación entre dispositivos (IoT) y protección de datos en red. Además, su arquitectura puede ejecutarse en sistemas virtualizados o contenedores.  
  En pocas palabras, combina visión artificial, IoT y seguridad digital, conceptos muy presentes en los sistemas digitales actuales.
</p>

<h2>AI-Based Energy Edge Platform, Systems, and Methods Having a Robotic Process Automation System</h2>
<p>
  <b>Patente:</b> US12332621B2<br>
  <b>Año:</b> 2025<br>
  <b>Entidad:</b> Strong Force EE Portfolio 2022 LLC<br><br>
  Esta patente plantea una plataforma de energía inteligente basada en IA, donde se usan sensores IoT para monitorear el consumo y robots de software (RPA) para automatizar procesos. Todo el sistema se gestiona en la <b>nube o en la “edge”</b>, es decir, de forma distribuida.  
  Se conecta con los temas de <b>virtualización</b>, <b>Docker</b>, y <b>redes IoT</b> porque la arquitectura está pensada para funcionar en entornos distribuidos y seguros. Incluso tiene relación con <b>ciberseguridad</b> energética.  
  Es un ejemplo claro de cómo la robótica y la IA se integran con sistemas digitales y automatización para mejorar la eficiencia energética.
</p>

<h2>Systems, Methods, Kits, and Apparatuses for Digital Product Network Systems and Biology-Based Value Chain Networks</h2>
<p>
  <b>Patente:</b> US20220245574A1<br>
  <b>Año:</b> 2022<br>
  <b>Entidad:</b> Strong Force VCN Portfolio 2019 LLC<br><br>
  Esta patente está enfocada en crear redes de cadena de valor digital donde se integran robots, drones y manufactura aditiva (impresión 3D). Es como una red inteligente de producción automatizada donde los robots pueden comunicarse entre sí y coordinar tareas.  
  En clase lo podemos asociar con <b>IoT</b> (robots interconectados), <b>ciberseguridad</b> (datos industriales protegidos), y <b>sistemas virtualizados</b> o basados en <b>Docker</b> (gestión de software en red).  
  Este tipo de plataformas son clave para la industria 4.0 y la robótica conectada, usando entornos digitales seguros y escalables.
</p>

<h2>Management System and Method Based on Internet of Things Blockchain Quantum Bit Artificial Intelligence</h2>
<p>
  <b>Patente:</b> CN109147880A<br>
  <b>Año:</b> 2019<br>
  <b>Entidad:</b> Guangdong Boyun Public Platform Network Technology Co., Ltd.<br><br>
  Esta patente combina <b>IoT</b>, <b>blockchain</b>, <b>computación cuántica</b> e <b>inteligencia artificial</b> para crear un sistema de gestión seguro y automatizado. Básicamente los dispositivos IoT envían información cifrada mediante blockchain, mientras la IA y los qubits procesan los datos.  
  Se relaciona directamente con los temas de <b>redes</b> y <b>ciberseguridad</b>, ya que busca proteger la comunicación entre dispositivos distribuidos. Además, plantea una aplicación de computación cuántica dentro de los sistemas digitales modernos.  
  Representa la evolución hacia redes inteligentes más seguras y autónomas.
</p>
