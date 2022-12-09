
# Control-de-Trabajos de Laboratorio

La siguiente documentación esta dirigida a las personas asistentes que son designadas a trabajar en este sistema.  


## Descripción del sistema
Sistema de control de las solicitudes de trabajo de los laboratorios del LanammeUCR incluyendo la trazabilidad de las muestras, ensayos, programaciones, informes y la administración financiera.
<br>

---

## Índice
* [Pre-requisitos](#Pre-requisitos)
* [Instalación](#Instalacion)
* [Ejecución](#Ejecucion)
* [Notas para asistentes](#Notas-para-asistentes)

---

<a name="Pre-requisitos"/>



## Pre-requisitos 📋
Herramientas necesarias para el proyecto
<ul>
<li>  
  <a href="https://visualstudio.microsoft.com/es/downloads/">Visual Studio</a>
  </li>
  <p>Framework utilizado para el desarrollo del proyecto.<br><br>
    <b>Tip:</b> Se recomienda utilizar versiones modernas</p>
  <li>  
  <a href="https://git-scm.com/downloads">Git</a> y <a href="https://desktop.github.com/">Github Desktop</a>
  </li>
  <p>Herramientas utilizadas para el versionamiento del proyecto</p>
  <li>  
  <a href="https://www.microsoft.com/es-es/sql-server/sql-server-downloads">SQL</a>
  </li>
  <p>Base de datos relacional utilizada en el proyecto</p>
  <li>
  <a href="https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16">SSMS</a>
  </li>
  <p>IDE utilizado para administrar, configurar y gestionar las bases de datos</p>
</ul>

---

<a name="Instalacion"/>

## Instalación 🔧

### Clonar repositorio

En el siguiente <a href="https://docs.github.com/es/repositories/creating-and-managing-repositories/cloning-a-repository" >link</a> se muestran las opciones que ofrece Github para clonar un repositorio y los pasos que hay que seguir si se realiza con Git o Github Desktop.


### Restaurar base de datos

En el siguiente enlace <a href="https://learn.microsoft.com/es-es/sql/relational-databases/backup-restore/quickstart-backup-restore-database?view=sql-server-ver16">link</a> se enseña paso a paso la restauración de una base de datos en SQL Server utilizando el SSMS.Asismísmo, la copia de la base de datos se llama "CTL.bak".


<a name="Ejecucion"/>


## Ejecución 🚀
En el siguente apartado se mostrán las configuraciones necesarias para ejecutar el proyecto y posibles soluciones a problemas que ocurran durante su ejecución.

* [Configuración](#Configuracion)
* [Posibles errores durante ejecución](#Posibles-errores)

---

<a name="Configuracion"/>

### Habilitar Web Forms en Visual Studio
Si se utilizan versiones modernas del Visual Studio, ya sea 2019 o 2022 debemos habilitar la opción de crear aplicaciones ASP.NET Web Forms.

Para ello abriremos el VisualStudioInstaller que aparece con el siguiente icono:

<div>
<p style = 'text-align:center;'>
<img src="https://github.com/Tony02030/ReadMeTest/blob/main/images/visualIcon.png"  width="200px" height="200px">
</p>
</div>
<br>

Buscamos el apartado "Modificar" del Visual Studio:
<div>
<p style = 'text-align:center;'>
<img src="https://github.com/Tony02030/ReadMeTest/blob/main/images/capt1.png"  width="750px">
</p>
</div>
<br>

En "Desarrollo de ASP.NET y web", buscamos la casilla que diga "Plantillas de proyecto y elemento de .Net Framework" y la seleccionamos.
<div>
<p style = 'text-align:center;'>
<img src="https://github.com/Tony02030/ReadMeTest/blob/main/images/capt2.png"  width="950px">
</p>
</div>
<br>

Al seleccionar la casilla, el botón "Cerrar" deberá cambiar a "Modificar". Le damos al botón y la instalación comenzaría. 

---

<h3>Configuración de archivos en proyecto</h3>

**Nota**: Las numeraciones de las líneas de código **NO** son exactas, son aproximaciones de donde podrían ubicarse.

#### ConexiónDatos.cs

Ubicación: AccesoDatos -> ConexiónDatos.cs <br>
Posible numeración de línea de código: 62 <br>

Buscamos la siguiente línea y la borramos: 

```
return new SqlConnection(System.Web.Configuration.WebConfigurationManager.ConnectionStrings["LOGINConnectionString"].ConnectionString);

```

Y agregamos las siguientes líneas:

```
//return new SqlConnection(System.Web.Configuration.WebConfigurationManager.ConnectionStrings["LOGINConnectionString"].ConnectionString);
          return null;
```

---

#### Web.config

Ubicación: CTL -> Web.config <br>
Posible numeración de línea de código: 63 <br>

Buscamos las etiquetas "\<connectionStrings>\...\</connectionStrings>" borramos la líneas dentro de ellas y agregamos las siguentes:

```
<add name="LOGINConnectionString" connectionString="Data Source=163.178.106.21;Initial Catalog=Login;User Id=sa;Password=sa123!!" providerName="System.Data.SqlClient"/>
<add name="CTLconnectionString" connectionString="Data Source=<local server>;Initial Catalog=CTL;Integrated Security=True" providerName="System.Data.SqlClient"/>
```

En el "CTLconnectionString" debemos cambiar el "Data Source" con la dirección de nuestro servidor local en SQL Server

---

#### Utilidades.cs

Ubicación: CTL -> Utilidades.cs <br>
Posible numeración de línea de código: 18 <br>

Buscamos la siguiente línea, la descomentamos y la reemplazamos por la ubicación de nuestro proyecto local

Ejemplo:

```
public static string path = "C:\\Users\\HP\\Documents\\GitHub\\Control-de-Trabajos-de-Laboratorio\\CTL";
```

Posible numeración de línea de código: 21 <br>
Buscamos la siguiente línea y la comentamos: 

```
//public static string path = "\\\\gaia\\AppFiles\\CTL\\Produccion\\";
```

---

#### Login.aspx.cs

Ubicación: CTL -> Login.aspx -> Login.aspx.cs <br>
Posible numeración de línea de código: 38 <br>

Buscamos las siguiente líneas y la comentamos:

```
//actualizarListaRoles();
//actualizarListaUsuarios();
```

Posible numeración de línea de código: 204 <br>
Buscamos las siguiente líneas y la comentamos:

```
//string dominName = string.Empty;
//string adPath = string.Empty;
//string nombreCompleto = string.Empty;
//string userName = txtUsuario.Text.Trim().ToUpper();
//string strError = string.Empty;
```

Posible numeración de línea de código: 210 <br>
Buscamos las siguientes líneas y las comentamos:

```
//foreach (string key in System.Configuration.ConfigurationManager.AppSettings.Keys)
        //{
```

Posible numeración de línea de código: 213 <br>
Buscamos las siguientes líneas y las comentamos:

```
// dominName = key.Contains("DirectoryDomain") ? System.Configuration.ConfigurationManager.AppSettings[key] : dominName;
                //adPath = key.Contains("DirectoryPath") ? System.Configuration.ConfigurationManager.AppSettings[key] : adPath;
                //if (!String.IsNullOrEmpty(dominName) && !String.IsNullOrEmpty(adPath))
                //{
                    //if (true == AuthenticateUser(dominName, userName, txtPassword.Text, adPath, out strError))
                    //{
```

Posible numeración de línea de código: 220 <br>
Buscamos las siguientes líneas y las comentamos:

```
//Session["login"] = userName;
```

Posible numeración de línea de código: 222 <br>
Buscamos las siguientes líneas y las comentamos:

```
//object[] datos = conexionServicios.loguearse(userName);
                        //if (datos[0] != null)
                        //{
                            //rol = Convert.ToInt32(datos[0].ToString());
                            //nombreCompleto = datos[1].ToString();

                            //Session["rol"] = rol;
                            //Session["nombreCompleto"] = nombreCompleto;

                            //Session["rol"] = 11;
                            //Session["nombreCompleto"] = "Ellen Rodriguez Castro";

                            //se busca el usuario para poder cargar los permisos que tiene
                            //Usuario usuario = new Usuario();

                            //usuario.nombreCompleto = nombreCompleto;

                            //usuario = usuarioServicios.getUsuarioPorNombreCompleto(usuario);

                            //Session["listaPermisosPagina"] = usuarioRolPaginaPermisoServicios.getPermisosPorUsuario(usuario);
```

Posible numeración de línea de código: 242 <br>
Agregamos el siguiente código después de las líneas anteriormente comentadas:

```
            rol = 2;
            //rol = 19;
            //String nombreCompleto = "Auditor";
            String nombreCompleto = "Leonardo Carrion Quiros";
            //String nombreCompleto = "Asistente UTI 05";

            Session["rol"] = rol;
            Session["nombreCompleto"] = nombreCompleto;
            Usuario usuario = new Usuario();

            usuario.nombreCompleto = nombreCompleto;

            usuario = usuarioServicios.getUsuarioPorNombreCompleto(usuario);

            Session["listaPermisosPagina"] = usuarioRolPaginaPermisoServicios.getPermisosPorUsuario(usuario);
```

Posible numeración de línea de código: 293 <br>
Buscamos las siguiente líneas y las comentamos:

```
                    //}
                       //else
                        //{
                            //lblNoUsuario.Visible = true;
                            //lblError.Visible = false;
                        //}
                    //}
                    //dominName = string.Empty;
                    //adPath = string.Empty;
                    //if (String.IsNullOrEmpty(strError)) break;
                //}
           //}
```


---


<a name="Posibles-errores"/>

### Posibles errores durante la ejecución
* Si aparece la siguiente linea en un error
```
Could not load file or assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies
```
Se debe descargar la herramienta <a href="https://www.microsoft.com/en-us/download/details.aspx?id=1491">AspNetMVC3ToolsUpdateSetup</a>, con solo su instalación el error debe desaparecer
<a name="Notas-para-asistentes"/>

---

## Notas para asistentes :technologist:
* Cada commit debe ser consultado y revisado antes de ser subido por la persona encargada.
* **NO** subir los archivos de configuración de su proyecto local, solo los archivos modificados manualmente.
* Cada modificación hecha en la base de datos debe ser añadida al repositorio, agregando un script con sus respectivas modificaciones.


