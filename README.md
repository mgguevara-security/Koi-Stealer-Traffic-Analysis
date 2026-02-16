\# INFORME DE INVESTIGACIÓN: INFECCIÓN POR KOI STEALER



\## 1. RESUMEN DEL INCIDENTE

Se ha detectado actividad maliciosa en la red interna vinculada al host `DESKTOP-RNV09AT`. El análisis del tráfico de red confirma una infección por el malware conocido como \*\*Koi Stealer\*\*, el cual está exfiltrando datos sensibles hacia un servidor en el extranjero.



---



\## 2. IDENTIFICACIÓN DEL EQUIPO AFECTADO

A través del análisis de los protocolos DHCP y ARP, se han determinado los siguientes datos del equipo comprometido:



\* \*\*Dirección IP:\*\* `172.17.0.99`

\* \*\*Dirección MAC:\*\* `18:3d:a2:b6:8d:c4`

\* \*\*Hostname:\*\* `DESKTOP-RNV09AT`



> \*\*EVIDENCIA A: Identificación de Red\*\*

> ![Evidencia Host](EVIDENCIA_HOST.png)



---



\## 3. IDENTIFICACIÓN DE LA VÍCTIMA (ANÁLISIS LDAP)

Mediante el análisis del tráfico LDAP (paquete #3019), se logró identificar la identidad del usuario a pesar de que la comunicación utilizaba integridad SASL.



\* \*\*Nombre de Usuario (ID):\*\* `afletcher`

\* \*\*Nombre Completo:\*\* `Andrew Fletcher`

\* \*\*Dominio:\*\* `bepositive.com`

\* \*\*Ruta LDAP (DN):\*\* `CN=Andrew Fletcher,CN=Users,DC=bepositive,DC=com`



> \*\*EVIDENCIA B: Identificación del Usuario\*\*

> ![Evidencia Usuario](Evidencia_Nombre_Completo_Usuario.png)



---



\## 4. ANÁLISIS DEL MALWARE Y EXFILTRACIÓN (C2)

Se identificó tráfico de salida persistente hacia una dirección IP reportada como maliciosa. El malware utiliza el método HTTP POST para subir información robada.



\* \*\*IP del Atacante (C2):\*\* `79.124.78.197` (Ubicación: Bulgaria)

\* \*\*Filtro de Wireshark:\*\* `http.request and ip.dst == 79.124.78.197`

\* \*\*Recurso de destino:\*\* `/foots.php`

\* \*\*User-Agent:\*\* `Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 10.0; ...)`



> \*\*EVIDENCIA C: Exfiltración de Datos\*\*

> ![Evidencia Malware](Evidencia_C2_Conexion_Malware.png)


---



\## 5. CONCLUSIONES Y RECOMENDACIONES

1\. \*\*Aislamiento:\*\* Se recomienda desconectar el host `172.17.0.99` de la red de inmediato.

2\. \*\*Remediación:\*\* Realizar un escaneo completo del equipo y proceder con el cambio de contraseñas de dominio para el usuario `Andrew afletcher`.

3\. \*\*Bloqueo:\*\* Bloquear en el Firewall perimetral cualquier comunicación hacia el rango de la IP `79.124.78.197`.


