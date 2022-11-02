
# Control-de-Trabajos de Laboratorio

Sistema de control de las solicitudes de trabajo de los laboratorios del LanammeUCR incluyendo la trazabilidad de las muestras, ensayos, programaciones, informes y la administración financiera.


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

En el siguiente enlace <a href="https://learn.microsoft.com/es-es/sql/relational-databases/backup-restore/quickstart-backup-restore-database?view=sql-server-ver16">link</a> se enseñan paso a paso la restauración de una base de datos en SQL Server utilizando el SSMS.


<a name="Ejecucion"/>


## Ejecución 🚀
En el siguente apartado se mostrán las configuraciones necesarias para ejecutar el proyecto y posibles soluciones a problemas que ocurran durante su ejecución.

* [Configuración](#Configuracion)
* [Posibles errores durante ejecución](#Posibles-errores)

---

<a name="Configuracion"/>

<h3>Configuración</h3>

**Nota**: Las numeraciones de las líneas de código **NO** son exactas, son aproximaciones de donde podrían ubicarse.

#### ConexiónDatos.cs

Ubicación: AccesoDatos -> ConexiónDatos.cs

Borramos la línea 62 y la cambios por la siguiente: 

```
//return new SqlConnection(System.Web.Configuration.WebConfigurationManager.ConnectionStrings["LOGINConnectionString"].ConnectionString);
          return null;
```
---

#### Web.config

Ubicación: CTL -> Web.config

Borramos las lineas desde la 63 hasta la 66 y agregamos las siguientes:

```
<add name="LOGINConnectionString" connectionString="Data Source=163.178.106.21;Initial Catalog=Login;User Id=sa;Password=sa123!!" providerName="System.Data.SqlClient"/>
<add name="CTLconnectionString" connectionString="Data Source=<local server>;Initial Catalog=CTL;Integrated Security=True" providerName="System.Data.SqlClient"/>

```

En el "CTLconnectionString" debemos cambiar el "Data Source" con la dirección de nuestro servidor local en SQL Server

---

#### Utilidades.cs

Ubicación: CTL -> Utilidades.cs

Descomentamos la linea 18 y la reemplazamos por la ubicación de nuestro proyecto local

Ejemplo:

```
public static string path = "C:\\Users\\HP\\Documents\\GitHub\\Control-de-Trabajos-de-Laboratorio\\CTL";
```

Comentamos la línea 21
```
//public static string path = "\\\\gaia\\AppFiles\\CTL\\Produccion\\";
```

---

#### Login.aspx.cs

Ubicación: CTL -> Login.aspx -> Login.aspx.cs

Comentamos las lineas 38 y 39

```
//actualizarListaRoles();
//actualizarListaUsuarios();
```

Comentamos desde la línea 204 hasta la 208

```
//string dominName = string.Empty;
//string adPath = string.Empty;
//string nombreCompleto = string.Empty;
//string userName = txtUsuario.Text.Trim().ToUpper();
//string strError = string.Empty;
```

Comentamos las líneas 210 y 211

```
//foreach (string key in System.Configuration.ConfigurationManager.AppSettings.Keys)
        //{
```

Comentamos desde la linea 213 a la 218

```
// dominName = key.Contains("DirectoryDomain") ? System.Configuration.ConfigurationManager.AppSettings[key] : dominName;
                //adPath = key.Contains("DirectoryPath") ? System.Configuration.ConfigurationManager.AppSettings[key] : adPath;
                //if (!String.IsNullOrEmpty(dominName) && !String.IsNullOrEmpty(adPath))
                //{
                    //if (true == AuthenticateUser(dominName, userName, txtPassword.Text, adPath, out strError))
                    //{
```

Comentamos la línea 220

```
//Session["login"] = userName;
```

Comentamos desde la línea 222 a la 241

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

Agregamos el siguiente código a partir de la línea 242

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

Comentamos desde la línea 293 hasta la 309

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


