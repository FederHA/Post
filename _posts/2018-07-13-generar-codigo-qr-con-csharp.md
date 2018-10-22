---
ID: 74
post_title: 'Generar codigo QR con c#'
author: Feder Huaman
post_excerpt: ""
layout: post
permalink: >
  http://federhuaman.pe.hu/programacion/generar-codigo-qr-con-csharp/
published: true
post_date: 2018-07-13 20:18:22
---
<!--vcv no format-->

<div class="vce-row-container">
  <div class="vce-row vce-row--col-gap-30 vce-row-columns--top vce-row-content--top" id="el-b67ec9c6" data-vce-do-apply="all el-b67ec9c6">
    <div class="vce-row-content" data-vce-element-content="true">
      <div class="vce-col vce-col--md-100p vce-col--xs-1 vce-col--xs-last vce-col--xs-first vce-col--sm-last vce-col--sm-first vce-col--md-last vce-col--lg-last vce-col--xl-last vce-col--md-first vce-col--lg-first vce-col--xl-first" id="el-105c3e19" data-vce-do-apply="background border el-105c3e19">
        <div class="vce-col-inner" data-vce-element-content="true" data-vce-do-apply="padding margin  el-105c3e19">
          <div class="vce-text-block">
            <div class="vce-text-block-wrapper vce" id="el-03476556" data-vce-do-apply="all el-03476556">
              <p>
                Hoy en día, los códigos QR se pueden ver en folletos, carteles, revistas, etc. Usted puede detectar fácilmente estos códigos de barras de dos dimensiones a tu alrededor. Los códigos QR permiten interactuar con el mundo a través de su smartphone. Específicamente, un QR Code extiende los datos a disposición de cualquier objeto físico y crean una medida digital para las operaciones de marketing.
              </p>
              
              <h3>
                ¿Que son los Códigos QR?
              </h3>
              
              <p>
                Los códigos QR, ( en inglés QR Code) son un tipo de códigos de barras bidimensionales. A diferencia de un código de barras convencional ( por ejemplo EAN-13, Código 3 de 9, UPC), la información está codificada dentro de un cuadrado, permitiendo almacenar gran cantidad de información alfanumérica.
              </p>
              
              <h3>
                ¿ Cómo generar un Código QR ?
              </h3>
              
              <p>
                Existen muchas librerias y formas para generar un código QR, para este post vamos a utilizar la librería 
              </p>
              
              <p>
                <a href="https://archive.codeplex.com/?p=qrcodenet" target="_blank" rel="noopener">Gma.QrCodeNet</a> podemos descargar desde el administrador de paquetes de .NET.
              </p>
              
              <h4>
                1. Crear proyecto en Visual Studio
              </h4>
              
              <p>
                Vamos crear un proyecto tipo aplicación Windows Forms en visual studio (yo tengo instalado el 2017 ). En mi caso al proyecto le pondré el nombre de <code>QRGenerator</code>
              </p>[caption id="attachment_88" align="aligncenter" width="700"]
              
              <img class="wp-image-88" src="|!|vcvUploadUrl|!|/2018/07/Crear-Proyecto-para-generar-QR.png" alt="Crear Proyecto para generar QR" width="700" height="481" /> Crear Proyecto para generar QR[/caption]<h4>
                2. Agregar la librería Después de haber creado nuestro proyecto vamos a agregar la librería
              </h4>
              
              <p>
                <a href="https://archive.codeplex.com/?p=qrcodenet" target="_blank" rel="noopener">Gma.QrCodeNet</a> ( Puedes agregar a un proyecto  que ya tienes desarrollado), para eso, damos click derecho en el nombre de nuestro proyecto creado->Administrar Paquetes NugGet, nos habrirá una ventana, nos dirigimos a la pestaña Examinar y buscamos la librería, como figura en la imagen.
              </p>[caption id="attachment_101" align="aligncenter" width="700"]
              
              <img class="wp-image-101" src="|!|vcvUploadUrl|!|/2018/07/Instalando-la-libreria-QrCodeNet-300x184.png" alt="Instalando la libreria QrCodeNet" width="700" height="428" /> Instalando la librería QrCodeNet[/caption]<p>
                Le damos click en instalar y la librería se agregará como referencia en nuestro proyecto.
              </p>
              
              <h4>
                3. Agregando controles para generar
              </h4>
              
              <p>
                Para mi caso utilizaré el formulario windows forms que se creó al momento de crear el proyecto. Vamos a diseñar el formulario con los controles necesarios, como se ve en la imagen.
              </p>[caption id="attachment_106" align="aligncenter" width="414"]
              
              <img class="size-full wp-image-106" src="|!|vcvUploadUrl|!|/2018/07/Agregando-controles-para-generar-el-codigo-QR-1.png" alt="Agregando controles para generar el codigo QR" width="414" height="369" /> Agregando controles para generar el código QR[/caption]<p>
                Ya tenemos diseñado nuestro formulario listo para escribir código.  Let's go !!!
              </p>
              
              <h4>
                7. Generando Código QR En el evento click del botón [ Generar QR ], vamos a escribir el siguiente código.
              </h4>
              
              <pre class="line-numbers" data-start="1"><code class="language-csharp">private void btnGenerarQR_Click(object sender, EventArgs e)
        {
            try
            {
                // Directorio donde se guardará la imagen QR
                string nombreArchivo = Application.StartupPath + $@"{txtCadena.Text}.png";
                // Si existe eliminamos el archivo               
                if (File.Exists(nombreArchivo))
                    File.Delete(nombreArchivo);
                QrEncoder qrEncoder = new QrEncoder(ErrorCorrectionLevel.Q);
                // Asingnamos el valor que queremos que tenga el QR
                QrCode qrCode = qrEncoder.Encode(txtCadena.Text);
                GraphicsRenderer renderer = new GraphicsRenderer(new FixedModuleSize(8, QuietZoneModules.Two), Brushes.Black, Brushes.White);
                using (FileStream stream = new FileStream(nombreArchivo, FileMode.Create))
                {
                    renderer.WriteToStream(qrCode.Matrix, ImageFormat.Png, stream);
                }
                picQR.Image = Image.FromFile(nombreArchivo);              
            }
            catch (Exception ex)
            {
               MessageBox.Show("Error en btnGenerarQR_Click(): " + ex.Message);
            }
        }</code></pre>
              
              <p>
                Esto es todo amigos, ya podemos generar nuestro código QR, puedes implementar en cualquier proyecto que estés desarrollando. El código completo del proyecto lo dejaré en
              </p>
              
              <p>
                <a href="https://github.com/FederHA/QRGenerator" target="_blank" rel="noopener">GitHub</a> Gracias por leer el artículo. Comparte con tus amigos. Hasta la próxima !!!!  
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!--vcv no format-->