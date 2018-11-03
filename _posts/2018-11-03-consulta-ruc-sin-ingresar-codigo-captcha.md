---
ID: 308
post_title: >
  Consulta RUC sin ingresar código
  captcha
author: Feder Huaman
post_excerpt: ""
layout: post
permalink: >
  http://federhuaman.pe.hu/programacion/consulta-ruc-sin-ingresar-codigo-captcha/
published: true
post_date: 2018-11-03 05:27:48
---
<!--vcv no format-->

<div class="vce-row-container">
  <div id="el-7433d429" class="vce-row vce-row--col-gap-30 vce-row-columns--top vce-row-content--top" data-vce-do-apply="all el-7433d429">
    <div class="vce-row-content" data-vce-element-content="true">
      <div id="el-9fb50701" class="vce-col vce-col--md-100p vce-col--xs-1 vce-col--xs-last vce-col--xs-first vce-col--sm-last vce-col--sm-first vce-col--md-last vce-col--lg-last vce-col--xl-last vce-col--md-first vce-col--lg-first vce-col--xl-first" data-vce-do-apply="background border el-9fb50701">
        <div class="vce-col-inner" data-vce-element-content="true" data-vce-do-apply="padding margin el-9fb50701">
          <div class="vce-text-block">
            <div id="el-43f9a7a1" class="vce-text-block-wrapper vce" data-vce-do-apply="all el-43f9a7a1">
              <h2>
                Consultar RUC directamente a SUNAT sin código captcha
              </h2> Hace poco estuve trabajando en un proyecto, en uno de los modulos tenía que contar con una opción para consultar el RUC,  lo cual consistía en ingresar el numero de RUC de la empresa y el sistema debe consultar directamente a SUNAT sin ingresar el código captcha. Después de tanta investigación en internet logro completar el requerimiento. Recuerda, la perseverancia y la capacidad de investigación nos hace grandes desarrolladores. Antes, se podía consulta el RUC en el portal de SUNAT sin ingresar el código captcha, pero, ahora se complica un poco con el famoso captcha. Antes la consulta era a la siguiente url: 
              
              <pre class="line-numbers"><code class="language-c">http://www.sunat.gob.pe/w/wapS01Alias?ruc={nímero de RUC}</code></pre> Ahora: 
              
              <pre class="line-numbers"><code class="language-c">http://www.sunat.gob.pe/cl-ti-itmrconsruc/jcrS00Alias</code></pre> Entonces, tuve que buscar un OCR(Reconocimiento óptico de caracteres) que me permita convertir la imagen captcha a un texto para mandar en la url de la consulta. La OCR se llama 
              
              <strong>Tesseract, </strong>lo mejor es que es de Open Source, lo que significa que es gratuito y de código libre. <a href="https://github.com/tesseract-ocr/tesseract">Código Fuente</a> Vamos a crear nuestro proyecto en Visual Studio y luego diseñamos el siguiente formulario. Para este ejemplo no voy a mostrar todos los datos de la empresa, solamente los datos necesarios. [caption id="attachment_311" align="alignnone" width="528"]<img class="size-full wp-image-311" src="http://federhuaman.pe.hu/wp-content/uploads/2018/11/Consulta-ruc-a-SUNAT.png" alt="Formulario de consulta ruc a SUNAT" width="528" height="213" /> Formulario de consulta RUC a SUNAT[/caption] Luego vamos a agregar las librerías necesarias desde el administrador de paquetes NuGet de nuestro proyecto. Para ello, <em>click derecho en nuestra solución -> Administrador de paquetes NuGet para la solución</em> y luego buscamos los siguientes paquetes: <ol>
                <li>
                  Agregar <strong>Tessnet2: </strong>Este es una extención de Tesseract para C#.
                </li>
                <li>
                  Agregar <strong>HtmlAgilityPack: </strong>Este es una librería que nos permite manipular Etiquetas HTML de manera muy simple.
                </li>
              </ol> Ya tenemos todo listo para escribir código. En el botón de consulta a SUNAT. Pegamos el siguiente código. 
              
              <pre class="line-numbers"><code class="language-csharp">           try
            {
                ConsultaRucSunat consultaRucSunat = new ConsultaRucSunat();
                btnConsultaSunat.Text = "Consultando...";
                Contribuyente contribuyente = await consultaRucSunat.ConsultaRuc(txtRuc.Text);
                txtRazonSocial.Text = contribuyente.RazonSocial;
                txtDirección.Text = contribuyente.Direccion;
                btnConsultaSunat.Text = "Consultar a SUNAT";
            }
            catch (Exception ex)
            {
                throw new Exception("Error en btnConsultaSunat_Click : " + ex.Message);
            }</code></pre> En el proyecto creamos una clase que se llama 
              
              <em>ConsultaRucSunat</em> y pegamos el siguiente código <pre class="line-numbers"><code class="language-csharp">    public class ConsultaRucSunat
    {
        string captcha = "";
        Encoding objEncoding = Encoding.GetEncoding("UTF-8");
        private static HttpClient httpClient = new HttpClient(new HttpClientHandler { UseProxy = true, });
        string rutaTessData = string.Empty;
        public ConsultaRucSunat()
        {
            // Inicializa por unica vez la direcciÓn base
            if(httpClient.BaseAddress == null)
                httpClient.BaseAddress = new Uri("http://www.sunat.gob.pe/");

            // IndicaNDO la ruta de la librería. 
            rutaTessData = Application.StartupPath + @"\tessdata\";
        }

        public async Task&lt;Contribuyente&gt; ConsultaRuc(string ruc)
        {
            Contribuyente contribuyente = new Contribuyente();
            try
            {
                ServicePointManager.DefaultConnectionLimit = 2;

                // Descarga la imagen captcha
                HttpResponseMessage responseMessage = await httpClient.GetAsync($"cl-ti-itmrconsruc/captcha?accion=image");
                if (responseMessage.IsSuccessStatusCode)
                {
                    Stream responseStream = await responseMessage.Content.ReadAsStreamAsync(); ;
                    var image = new Bitmap(responseStream);
                    var ocr = new Tesseract();

                    // Indicamos la ruta de la libreria
                    ocr.Init(rutaTessData, "eng", false);

                    // Convertir la imagen a texto plano
                    var result = ocr.DoOCR(image, Rectangle.Empty);
                    foreach (Word word in result)
                    {
                        captcha += word.Text;
                    }

                }
                else
                    return null;

                // Consulta el RUC enviando el codigo captcha
                var ConsultaRuc = await httpClient.GetAsync($"cl-ti-itmrconsruc/jcrS00Alias?accion=consPorRuc&nroRuc={ruc}&codigo={captcha.Trim().ToUpper()}&tipodocumento=1");

                // Si la consulta es exitosa
                if (ConsultaRuc.IsSuccessStatusCode)
                {
                    string msg = string.Empty;

                    // Libreria que permite trabajar con etiquetas HTML
                    HtmlAgilityPack.HtmlDocument document = new HtmlAgilityPack.HtmlDocument();

                    // Carga el contenido html de la consulta
                    document.LoadHtml(await ConsultaRuc.Content.ReadAsStringAsync());
                    var NodeTable = document.DocumentNode
                                            .SelectNodes("//table")
                                            .FirstOrDefault();
                    if (NodeTable != null)
                    {
                        var listNodeTr = NodeTable.Elements("tr").ToArray();
                        if (listNodeTr != null)
                        {
                            // Extrae los valores de las celdas de la tabla. 
                            var nodeRazonSocial = listNodeTr[0].Elements("td").ToArray();
                            if (nodeRazonSocial != null)
                            {
                                string ConsultaCliente = LimpiarEspacios(nodeRazonSocial[1].InnerHtml.Trim());
                                contribuyente.RUC = ConsultaCliente.Substring(0, 11).Trim();
                                contribuyente.RazonSocial = ConsultaCliente.Substring(13, ConsultaCliente.Length - 13).Trim();
                            }
                            var nodeDireccion = listNodeTr[6].Elements("td").ToArray();
                            if (ruc.StartsWith("10"))
                            {
                                nodeDireccion = listNodeTr[7].Elements("td").ToArray();
                            }
                            if (nodeDireccion != null)
                            {
                                string ConsultaDireccion = LimpiarEspacios(nodeDireccion[1].InnerHtml.Trim());
                                contribuyente.Direccion = ConsultaDireccion.Trim();
                            }
                        }
                    }
                }

            }
            catch (Exception ex)
            {              
            }
            return await Task.Run(() =&gt; contribuyente);
        }

        private string LimpiarEspacios(string cadena)
        {
            while (cadena.Contains("  "))
            {
                cadena = cadena.Replace("  ", " ");
            }
            return cadena;
        }
    }</code></pre>
              
              <code class="language-csharp"></code> Listo, ya podemos consultar el RUC directamente a SUNAT. [caption id="attachment_314" align="alignnone" width="584"]<img class="size-full wp-image-314" src="http://federhuaman.pe.hu/wp-content/uploads/2018/11/Consulta-ruc-a-SUNAT-con-CSHAP.png" alt="Consulta ruc a SUNAT - con CSHAP" width="584" height="204" /> Consulta RUC a SUNAT - Resultado[/caption] Si tienes un proyecto existente simplemente puedes copiar la clase a tu proyecto y llamar el método <em>ConsultaRuc(ruc).</em> Código fuente en mi <a href="https://github.com/FederHuaman/AppConsultaRucSunat">repositorio GitHub</a> Gracias por leer el post. Comparte !!!
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!--vcv no format-->