---
title: Proporcionar datos al soporte de GitHub
intro: 'Since {% data variables.contact.github_support %} doesn''t have access to your environment, we sometimes require some additional information from you.'
shortTitle: Providing data
versions:
  ghes: '*'
redirect_from:
  - /enterprise/admin/guides/installation/troubleshooting
  - /enterprise/admin/articles/support-bundles
  - /enterprise/admin/guides/enterprise-support/providing-data-to-github-enterprise-support
  - /enterprise/admin/enterprise-support/providing-data-to-github-support
  - /admin/enterprise-support/providing-data-to-github-support
  - /admin/enterprise-support/receiving-help-from-github-support/providing-data-to-github-support
topics:
  - Support
---

## About diagnostic files and support bundles

{% data variables.contact.github_support %} may ask you to provide additional data in the form of sanitized log files. There are three types of log file you may be asked to provide.

Los archivos de diagnóstico contienen información sobre los ajustes y de una instancia de {% data variables.product.prodname_ghe_server %} y los paquetes de soporte de ambiente contienen información de diagnóstico y bitácoras de los dos días anteriores y los paquetes de soporte extendido también contienen información de diagnóstico y bitácoras, pero de los siete días anteriores.

## Crear y compartir archivos de diagnóstico

Diagnostic files are an overview of a {% data variables.product.prodname_ghe_server %} instance's settings and environment that contains:

- Información de licencia de cliente, incluido el nombre de la empresa, fecha de validez y cantidad de licencias de usuario
- Números de versión y SHAs
- Arquitectura VM
- Nombre de host, modo privado, entorno de SSL
- Cargar y procesar listas
- Parámetros de red
- Método y detalles de autenticación
- Número de repositorios, usuarios y otros datos de instalación

Puedes descargar el diagnóstico para tu instancia desde la {% data variables.enterprise.management_console %} o al ejecutar la utilidad de la línea de comando `ghe-diagnostics`.

### Crear un archivo de diagnóstico desde {% data variables.enterprise.management_console %}

Puedes usar este método si no tienes tu clave SSH fácilmente disponible.

{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.management-console %}
{% data reusables.enterprise_management_console.type-management-console-password %}
{% data reusables.enterprise_management_console.support-link %}
5. Haz clic en **Download diagnostics info** (Descargar información de diagnóstico).

### Crear un archivo de diagnóstico mediante SSH

Puedes usar este método sin iniciar sesión en {% data variables.enterprise.management_console %}.

Usa la utilidad de la línea de comando [ghe-diagnostics](/enterprise/{{ currentVersion }}/admin/guides/installation/command-line-utilities#ghe-diagnostics) para recuperar el diagnóstico para tu instancia.

```shell
$ ssh -p122 admin@<em>hostname</em> -- 'ghe-diagnostics' > diagnostics.txt
```

## Crear y compartir paquetes de soporte

Después de que emites tu solicitud de soporte, podríamos pedirte que compartas un paquete de soporte con nuestro equipo. El paquete de soporte es un archivo tar comprimido en gzip que incluye diagnósticos y registros importantes desde tu instancia, como:

- Registros relacionados con la autenticación que pueden resultar útiles al solucionar problemas de errores de autenticación, o configurar LDAP, CAS o SAML
- Registro {% data variables.enterprise.management_console %}
- `github-logs/exceptions.log`: Información sobre 500 errores encontrados en el sitio
- `github-logs/audit.log`: registros de auditoría {% data variables.product.prodname_ghe_server %}
- `babeld-logs/babeld.log`: registros proxy Git
- `system-logs/haproxy.log`: registros HAProxy
- `elasticsearch-logs/github-enterprise.log`: registros Elasticsearch
- `configuration-logs/ghe-config.log`: registros de configuración {% data variables.product.prodname_ghe_server %}
- `collectd/logs/collectd.log`: registros Collectd
- `mail-logs/mail.log`: registros de entrega por correo electrónico SMTP

Para obtener más información, consulta "[Audit logging](/enterprise/{{ currentVersion }}/admin/guides/installation/audit-logging) (Registro de auditoría".

Los paquetes de soporte incluyen registros de los dos últimos días. Para obtener registros de los últimos siete días, puedes descargar un paquete de soporte extendido. Para obtener más información, consulta "[Crear y compartir paquete de soporte extendido](#creating-and-sharing-extended-support-bundles)".

{% tip %}

**Sugerencias:** Cuando te comuniques con {% data variables.contact.github_support %}, recibirás un correo electrónico de confirmación con un enlace de referencia del ticket. Si {% data variables.contact.github_support %} te pide que cargues un paquete de soporte, puedes usar el enlace de referencia del ticket para cargar el paquete de soporte.

{% endtip %}

### Crear un paquete de soporte desde la {% data variables.enterprise.management_console %}

Puedes usar estos pasos para crear y compartir un paquete de soporte si puedes acceder a la {% data variables.enterprise.management_console %} basada en la web y tienes acceso a internet de salida.

{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.management-console %}
{% data reusables.enterprise_management_console.type-management-console-password %}
{% data reusables.enterprise_management_console.support-link %}
5. Haz clic en **Download support bundle** (Descargar paquete de soporte).
{% data reusables.enterprise_enterprise_support.sign-in-to-support %}
{% data reusables.enterprise_enterprise_support.upload-support-bundle %}

### Crear un paquete de soporte mediante SSH

Puedes utilizar estos pasos para crear y compartir un paquete de soporte si tienes acceso por SSH a {% data variables.product.product_location %} y cuentas con acceso externo a internet.

{% data reusables.enterprise_enterprise_support.use_ghe_cluster_support_bundle %}

1. Descargar el paquete de soporte mediante SSH:
  ```shell
  $ ssh -p 122 admin@<em>hostname</em> -- 'ghe-support-bundle -o' > support-bundle.tgz
  ```
  Para obtener más información acerca del comando `ghe-support-bundle`, consulta "[Utilidades de la línea de comandos](/enterprise/admin/guides/installation/command-line-utilities#ghe-support-bundle)".
{% data reusables.enterprise_enterprise_support.sign-in-to-support %}
{% data reusables.enterprise_enterprise_support.upload-support-bundle %}

### Cargar un paquete de soporte utilizando tu cuenta empresarial

{% data reusables.enterprise-accounts.access-enterprise-on-dotcom %}
{% data reusables.enterprise-accounts.settings-tab %}
3. En la barra lateral izquierda, da clic en **Licenciamiento empresarial**. ![Screenshot showing "Enterprise licensing" link in the enterprise account settings sidebar.](/assets/images/help/enterprises/enterprise-licensing-tab.png)
4. Debajo de "Ayuda de {% data variables.product.prodname_enterprise %}", da clic en **Cargar un paquete de soporte**. ![Screenshot showing "Upload a support bundle link".](/assets/images/enterprise/support/upload-support-bundle.png)
5. Debajo de "Selecciona una cuenta empresarial", selecciona la cuenta asociada al paquete de soporte del menú desplegable. ![Screenshot showing the dropdown menu to select the support bundle's enterprise account.](/assets/images/enterprise/support/support-bundle-account.png)
6. Debajo de "Cargar un paquete de soporte para {% data variables.contact.enterprise_support %}", para seleccionar tu paquete de soporte, da clic en **Elegir archivo**, o arrastra tu archivo de paquete de soporte hacia **Escoger archivo**. ![Screenshot showing the "Choose file" button to upload a support bundle file.](/assets/images/enterprise/support/choose-support-bundle-file.png)
7. Da clic en **Cargar**.

### Cargar paquete de soporte mediante SSH

Puedes cargar directamente un paquete de soporte a nuestro servidor si:
- Tienes acceso de SSH a {% data variables.product.product_location %}.
- Se permiten las conexiones HTTPS salientes por el puerto 443 TCP desde {% data variables.product.product_location %} hacia _enterprise-bundles.github.com_ y _esbtoolsproduction.blob.core.windows.net_.

1. Cargar el paquete a nuestro servidor de paquete de soporte:
  ```shell
  $ ssh -p122 admin@<em>hostname</em> -- 'ghe-support-bundle -u'
  ```

## Crear y compartir paquetes de soporte extendido

Los paquetes de soporte incluyen registros de los últimos dos días, mientras que los paquetes de soporte _extendidos_ incluyen registros de los últimos siete días. Si los eventos que {% data variables.contact.github_support %} estás investigando se produjeron hace más de dos días, es posible que te pidamos que compartas un paquete de soporte extendido. Deberás tener acceso a SSH para descargar un soporte extendido, no puedes descargar un paquete extendido desde {% data variables.enterprise.management_console %}.

Para evitar que los paquetes sean demasiado grandes, solo pueden contener registros que no hayan sido rotados y comprimidos. La rotación de los registros en {% data variables.product.prodname_ghe_server %} se produce en diferentes frecuencias (diarias o semanales) para los diferentes archivos de registro, según el tamaño que pretendamos que tengan los registros.

### Crear un paquete de soporte extendido mediante SSH

Puedes utilizar estos pasos para crear y compartir un paquete de soporte extendido si tienes acceso de SSH a {% data variables.product.product_location %} y si tienes acceso externo a internet.

1. Descarga el paquete de soporte extendido mediante SSH al agregar el marcador `-x` al comando `ghe-support-bundle`:
  ```shell
  $ ssh -p 122 admin@<em>hostname</em> -- 'ghe-support-bundle -o -x' > support-bundle.tgz
  ```
{% data reusables.enterprise_enterprise_support.sign-in-to-support %}
{% data reusables.enterprise_enterprise_support.upload-support-bundle %}

### Cargar un paquete de soporte extendido directamente usando SSH

Puedes cargar directamente un paquete de soporte a nuestro servidor si:
- Tienes acceso de SSH a {% data variables.product.product_location %}.
- Se permiten las conexiones HTTPS salientes por el puerto 443 TCP desde {% data variables.product.product_location %} hacia _enterprise-bundles.github.com_ y _esbtoolsproduction.blob.core.windows.net_.

1. Cargar el paquete a nuestro servidor de paquete de soporte:
  ```shell
  $ ssh -p122 admin@<em>hostname</em> -- 'ghe-support-bundle -u -x'
  ```

## Leer más

- "[About GitHub Support](/support/learning-about-github-support/about-github-support)"
