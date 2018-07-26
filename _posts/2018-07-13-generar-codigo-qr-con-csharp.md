---
ID: 74
post_title: 'Generar codigo QR con c#'
author: feder
post_excerpt: ""
layout: post
permalink: >
  http://federhuaman.pe.hu/programacion/generar-codigo-qr-con-csharp/
published: true
post_date: 2018-07-13 20:18:22
---
Hoy en día, los códigos QR se pueden ver en folletos, carteles, revistas, etc. Usted puede detectar fácilmente estos códigos de barras de dos dimensiones a tu alrededor. Los códigos QR permiten interactuar con el mundo a través de su smartphone. Específicamente, un QR Code extiende los datos a disposición de cualquier objeto físico y crean una medida digital para las operaciones de marketing. 
### ¿Que son los Códigos QR?
Los códigos QR, ( en inglés QR Code) son un tipo de códigos de barras bidimensionales. A diferencia de un código de barras convencional ( por ejemplo EAN-13, Código 3 de 9, UPC), la información está codificada dentro de un cuadrado, permitiendo almacenar gran cantidad de información alfanumérica. 

### ¿ Cómo generar un Código QR ? 
Existen muchas librerias y formas para generar un código QR, para este post vamos a utilizar la librería 

<a href="https://archive.codeplex.com/?p=qrcodenet" target="_blank" rel="noopener">Gma.QrCodeNet</a> podemos descargar desde el administrador de paquetes de .NET. 
#### 1. Crear proyecto en Visual Studio
Vamos crear un proyecto tipo aplicación Windows Forms en visual studio (yo tengo instalado el 2017 ). En mi caso al proyecto le pondré el nombre de `QRGenerator` [caption id="attachment_88" align="aligncenter" width="700"]<img class="wp-image-88" src="http://federhuaman.pe.hu/wp-content/uploads/2018/07/Crear-Proyecto-para-generar-QR.png" alt="Crear Proyecto para generar QR" width="700" height="481" /> Crear Proyecto para generar QR[/caption]   
#### 2. Agregar la librería Después de haber creado nuestro proyecto vamos a agregar la librería 

<a href="https://archive.codeplex.com/?p=qrcodenet" target="_blank" rel="noopener">Gma.QrCodeNet</a> ( Puedes agregar a un proyecto  que ya tienes desarrollado), para eso, damos click derecho en el nombre de nuestro proyecto creado->Administrar Paquetes NugGet, nos habrirá una ventana, nos dirigimos a la pestaña Examinar y buscamos la librería, como figura en la imagen. [caption id="attachment_101" align="aligncenter" width="700"]<img class="wp-image-101" src="http://federhuaman.pe.hu/wp-content/uploads/2018/07/Instalando-la-libreria-QrCodeNet-300x184.png" alt="Instalando la libreria QrCodeNet" width="700" height="428" /> Instalando la librería QrCodeNet[/caption] Le damos click en instalar y la librería se agregará como referencia en nuestro proyecto. 
#### 3\. Agregando controles para generar
Para mi caso utilizaré el formulario windows forms que se creó al momento de crear el proyecto. Vamos a diseñar el formulario con los controles necesarios, como se ve en la imagen. [caption id="attachment_106" align="aligncenter" width="414"]

<img class="size-full wp-image-106" src="http://federhuaman.pe.hu/wp-content/uploads/2018/07/Agregando-controles-para-generar-el-codigo-QR-1.png" alt="Agregando controles para generar el codigo QR" width="414" height="369" /> Agregando controles para generar el código QR[/caption] Ya tenemos diseñado nuestro formulario listo para escribir código.  Let's go !!! 
#### 7\. Generando Código QR En el evento click del botón [ Generar QR ], vamos a escribir el siguiente código. 

<pre class="prettyprint">private void btnGenerarQR_Click(object sender, EventArgs e)
        {
            try
            {
                // Directorio donde se guardará la imagen QR
                string nombreArchivo = Application.StartupPath + $@"\{txtCadena.Text}.png";
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
        }
</pre> Esto es todo amigos, ya podemos generar nuestro código QR, puedes implementar en cualquier proyecto que estés desarrollando. El código completo del proyecto lo dejaré en 

<a href="https://github.com/FederHA/QRGenerator" target="_blank" rel="noopener">GitHub</a> Gracias por leer el artículo. Comparte con tus amigos. Hasta la próxima !!!!  
