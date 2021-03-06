---
ID: 135
post_title: >
  ¿Qué es un control de versiones, y por
  qué debería ser importarte?
author: Feder Huaman
post_excerpt: ""
layout: post
permalink: >
  http://federhuaman.pe.hu/programacion/que-es-un-control-de-versiones-y-por-que-deberia-ser-importarte/
published: true
post_date: 2018-07-26 19:39:28
---
<!--vcv no format-->

<div class="vce-row-container">
  <div class="vce-row vce-row--col-gap-30 vce-row-columns--top vce-row-content--top" id="el-4785e5ea" data-vce-do-apply="all el-4785e5ea">
    <div class="vce-row-content" data-vce-element-content="true">
      <div class="vce-col vce-col--md-100p vce-col--xs-1 vce-col--xs-last vce-col--xs-first vce-col--sm-last vce-col--sm-first vce-col--md-last vce-col--lg-last vce-col--xl-last vce-col--md-first vce-col--lg-first vce-col--xl-first" id="el-ac2a223d" data-vce-do-apply="background border el-ac2a223d">
        <div class="vce-col-inner" data-vce-element-content="true" data-vce-do-apply="padding margin  el-ac2a223d">
          <div class="vce-text-block">
            <div class="vce-text-block-wrapper vce" id="el-9a161e55" data-vce-do-apply="all el-9a161e55">
              <p>
                Un control de versiones es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo, de modo que puedas recuperar versiones específicas más adelante. Esto puedes hacer casi en cualquier tipo de archivo que encuentres en una computadora.
              </p>
              
              <p>
                Si eres diseñador gráfico o de web y quieres mantener cada versión de una imagen o diseño (es algo que sin duda vas a querer), usar un sistema de control de versiones (VCS por sus siglas en inglés) es una decisión muy acertada. Dicho sistema te permite regresar a versiones anteriores de tus archivos, regresar a una versión anterior del proyecto completo, comparar cambios a lo largo del tiempo, ver quién modificó por última vez algo que pueda estar causando problemas, ver quién introdujo un problema y cuándo, y mucho más
              </p>
              
              <h2>
                Tipos de sistemas de control de versiones
              </h2>
              
              <p>
                Tenemos 3 tipos de sistemas de control de versiones:<br /> - Sistemas de control de versiones locales<br /> - Sistemas de control de versiones centralizados<br /> - Sistemas de control de versiones distribuidos
              </p>
              
              <h3>
                Sistemas de Control de Versiones Locales
              </h3>
              
              <p>
                Un método de control de versiones usado por muchas personas es copiar los archivos a otro directorio (quizás indicando la fecha y hora en que lo hicieron, si son ingeniosos).
              </p>
              
              <p>
                Para afrontar este problema los programadores desarrollaron hace tiempo VCS locales que contenían una simple base de datos en la que se llevaba el registro de todos los cambios realizados a los archivos.
              </p>
              
              <p>
                Una de las herramientas de control de versiones más popular fue un sistema llamado RCS, que todavía podemos encontrar en muchas de las computadoras actuales. Incluso el famoso sistema operativo Mac OS X incluye el comando RCS cuando instalas las herramientas de desarrollo
              </p>
              
              <h3>
                Sistemas de Control de Versiones Centralizados
              </h3>
              
              <p>
                El siguiente gran problema con el que se encuentran las personas es que necesitan colaborar con desarrolladores en otros sistemas.
              </p>
              
              <p>
                Los sistemas de Control de Versiones Centralizados (CVCS por sus siglas en inglés) fueron desarrollados para solucionar este problema. Estos sistemas, como CVS, Subversion, y Perforce, tienen un único servidor que contiene todos los archivos versionados, y varios clientes descargan los archivos desde ese lugar central. Este ha sido el estándar para el control de versiones por muchos años.
              </p>
              
              <p>
                Esta configuración ofrece muchas ventajas, especialmente frente a VCS locales. Por ejemplo, todas las personas saben hasta cierto punto en qué están trabajando los otros colaboradores del proyecto. Los administradores tienen control detallado sobre qué puede hacer cada usuario, y es mucho más fácil administrar un CVCS que tener que lidiar con bases de datos locales en cada cliente.
              </p>
              
              <p>
                Sin embargo, esta configuración también tiene serias desventajas. La más obvia es el punto único de fallo que representa el servidor centralizado. Si ese servidor se cae durante una hora, entonces durante esa hora nadie podrá colaborar o guardar cambios en archivos en los que hayan estado trabajando. Si el disco duro en el que se encuentra la base de datos central se corrompe, y no se han realizado copias de seguridad adecuadamente, se perderá toda la información del proyecto, con excepción de las copias instantáneas que las personas tengan en sus máquinas locales. Los VCS locales sufren de este mismo problema: Cuando tienes toda la historia del proyecto en un mismo lugar, te arriesgas a perderlo todo.
              </p>
              
              <h3>
                Sistemas de Control de Versiones Distribuidos
              </h3>
              
              <p>
                Los sistemas de Control de Versiones Distribuidos (DVCS por sus siglas en inglés) ofrecen soluciones para los problemas que han sido mencionados. En un DVCS (como Git, Mercurial, Bazaar o Darcs), los clientes no solo descargan la última copia instantánea de los archivos, sino que se replica completamente el repositorio. De esta manera, si un servidor deja de funcionar y estos sistemas estaban colaborando a través de él, cualquiera de los repositorios disponibles en los clientes puede ser copiado al servidor con el fin de restaurarlo. Cada clon es realmente una copia completa de todos los datos.
              </p>
              
              <p>
                Además, muchos de estos sistemas se encargan de manejar numerosos repositorios remotos con los cuales pueden trabajar, de tal forma que puedes colaborar simultáneamente con diferentes grupos de personas en distintas maneras dentro del mismo proyecto. Esto permite establecer varios flujos de trabajo que no son posibles en sistemas centralizados, como pueden ser los modelos jerárquicos.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!--vcv no format-->