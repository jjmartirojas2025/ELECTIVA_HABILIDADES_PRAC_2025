# **<p align="center">:imp::rotating_light::skull:DEFENSA EN PROFUNDIDAD:skull::rotating_light::imp:</p>**
# **<p align="center">:warning: FORTALEZA DIGITAL DE TECHSOLUTIONS CORP. :warning:</p>**
![EQUIPO DE HACKING ÉTICO MGOT](https://media.licdn.com/dms/image/v2/D4E12AQGtgZUaecTDtg/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1704959664316?e=2147483647&v=beta&t=PovZR5gg6Mznz1sZ-ErCfzXwaOfQl0qAr_ZpUeM_YBM)

# <p align="center">Grupo :shipit::computer:**"Q" CYBERTEAM**:computer::shipit: </p>

- [X] MY. CARLOS URIBE :airplane:
- [X] MY. MARIO GÓMEZ :airplane:
- [X] MY. DANIEL TORRES :airplane:
- [X] MY. MANUEL REY :boom::tractor:
- [X] MY. ARTURO MAHECHA :boom::tractor:
- [X] CC. JOHAN MARTINEZ :anchor:
- [X] CC. RUBEN CONTRERAS :anchor:

![Cyber](https://i.gifer.com/origin/46/46400cbacaf8eb1b36a89cdcd7da6740_w200.webp) ![Cyber](https://i.gifer.com/origin/5a/5ab98406cc6c8fbba9ddb014c2bcdb80_w200.webp)

A lo largo del siguiente trabajo, exploraremos un enfoque integral para fortalecer nuestra postura de seguridad digital mediante capas superpuestas de protección.
---
![amenazas](https://github.com/user-attachments/assets/a36aa81f-43d5-4f2c-9b77-398b82fe8a81)

# :one:	Análisis de Amenazas y Vulnerabilidades

Las vulnerabilidades explotadas incluyen la falta de concienciación del personal, filtros de correo insuficientes (spam, DMARC), ausencia de mecanismos de doble factor (MFA) y contraseñas débiles. Según informes, alrededor del 74 % de los ataques comienzan por errores humanos, por ejemplo dar clic en enlaces maliciosos, por lo que la carencia de formación y controles antiphishing es crítica.

**:white_check_mark:1.1.	Amenazas identificadas:**

:small_blue_diamond:Phishing dirigido: correos simulando comunicaciones internas para capturar credenciales.

:small_blue_diamond:Vulnerabilidad de día cero: software de gestión desactualizado expuesto en la DMZ (Zona Desmilitarizada).

:small_blue_diamond:Malware desde redes sociales: vector alterno mediante ingeniería social.

:small_blue_diamond:Movimiento lateral y persistencia: escaneo de red interna, creación de cuentas ocultas y tareas automatizadas.

:small_blue_diamond:Exfiltración y ransomware: tráfico anómalo a IPs externas y cifrado de archivos con notas de rescate.

**:white_check_mark:1.2.	Vulnerabilidades técnicas:**

:small_blue_diamond:Ausencia de MFA (Autenticación Multifactor): Permite que un atacante con solo las credenciales comprometidas tenga acceso total. Esto contradice lo recomendado por NIST (Instituto Nacional de Estándares y Tecnología) SP 800-63B.

:small_blue_diamond:Software no parcheado: La falta de actualizaciones expone sistemas a vulnerabilidades conocidas, como se describe en NIST SP 800-40.

:small_blue_diamond:Falta de segmentación interna: Permite el movimiento lateral libre dentro de la red tras una intrusión inicial, contrario al enfoque Zero Trust (Confianza Cero) descrito en NIST SP 800-207.

:small_blue_diamond:Control de acceso débil: El uso de privilegios excesivos y cuentas mal gestionadas facilita la escalada de privilegios, contraviniendo ISO/IEC (Organización Internacional de Normalización / Comisión Electrotécnica Internacional) 27001 A.9.

:small_blue_diamond:Deficiencias en monitoreo y detección: La ausencia de registros detallados y correlación de eventos limita la capacidad de detectar y contener ataques, como alerta NIST SP 800-92.

Normas de referencia: NIST SP 800-30, 40, 63B, 92, 207; ISO/IEC 27005, OWASP (Open Worldwide Application Security Project) Top 10.

---
![2](https://github.com/user-attachments/assets/ce0c0d68-d3ac-4295-9450-e6aa4efeddba)

# :two:	Principios de Defensa en Profundidad

La defensa en profundidad busca capas superpuestas de controles de seguridad para que la falla de uno no comprometa todo el sistema. La implementación de múltiples productos y prácticas de seguridad puede ayudar a detectar y prevenir ataques a medida que van surgiendo, permitiendo mitigar eficazmente una amplia gama de amenazas.
En la práctica, TechSolutions debe aplicar controles físicos, técnicos y administrativos en cada nivel de su infraestructura (perímetro, red interna, endpoints, aplicaciones, datos, identidad, operaciones).

**:white_check_mark:2.1.	Controles redundantes:** Múltiples medidas de seguridad en cada capa del entorno de TI (Tecnologías de la Información). Si una medida falla, otras mitigan el riesgo. Aplicable según NIST SP 800-53 CA-7 (monitoreo continuo) y SI-3 (protección contra código malicioso).

**:white_check_mark:2.2.	Segmentación y control de accesos:** Separar lógicamente redes y servicios, limitar comunicaciones innecesarias entre dominios. NIST SP 800-207 (Zero Trust) y CIS (Center for Internet Security) Control 14 recomiendan microsegmentación para evitar desplazamientos laterales.

**:white_check_mark:2.3.	Mecanismos de detección y respuesta:** Uso de SIEM (Gestión de Información y Eventos de Seguridad), EDR (Detección y Respuesta en el Endpoint) y NDR (Detección y Respuesta en la Red) para capturar y analizar eventos. NIST SP 800-137 y SP 800-61 Rev. 2 guían sobre monitoreo continuo y respuesta estructurada.

**:white_check_mark:2.4.	Principio de menor privilegio:** Usuarios y procesos deben tener acceso mínimo necesario. NIST SP 800-53 AC-6 e ISO/IEC 27001 A.9.1.2 obligan a aplicar controles de privilegios rigurosos.

**:white_check_mark:2.5.	Recuperación y continuidad operativa:** Capacidad de volver a operar después de un incidente. Requiere backups (copias de seguridad) verificados, redundancia de infraestructura y planes DRP (Planes de Recuperación ante Desastres) según NIST SP 800-34 Rev.1 e ISO 27031.

**:white_check_mark:2.6.	Cultura y procesos:** Además de soluciones técnicas, la concienciación del personal y procedimientos claros (políticas de seguridad, planes de respuesta) son capas defensivas críticas. La formación continua y auditorías internas aseguran que las medidas técnicas funcionen correctamente y que el equipo sepa cómo reaccionar ante incidentes.

*Normas de referencia: NIST SP 800-53 Rev. 5, 207, 137, 34; CIS Controls v8; ISO/IEC 27001, 27031.*

---
![image](https://github.com/user-attachments/assets/526ce61b-b306-413d-98a4-548a1ef488ab)

# :three:	Capas de Defensa Propuestas

**:white_check_mark:3.1.	Capa 1: Perímetro/Red Externa**

Medidas Técnicas

:small_blue_diamond:NGFW (Firewall de Nueva Generación): Filtrado de tráfico con inspección profunda de paquetes (NIST SP 800-41).

:small_blue_diamond:IDS/IPS (Sistemas de Detección/Prevención de Intrusos): Detecta intentos de intrusión y bloquea tráfico sospechoso.

:small_blue_diamond:WAF (Firewall de Aplicaciones Web): Filtrado HTTP para proteger APIs (Interfaces de Programación de Aplicaciones) y aplicaciones web ante OWASP Top 10.

:small_blue_diamond:DMZ (Zona Desmilitarizada): Contención de servicios expuestos al público, evitando que una intrusión llegue a la red interna (ISO/IEC 27033).

:small_blue_diamond:Filtrado DNS (Sistema de Nombres de Dominio) y reputación IP: Prevención de comunicaciones maliciosas (CIS Control 9).
Medidas Administrativas

*Políticas de seguridad perimetral (segregación de DMZ, revisión de reglas de firewall periódicamente); monitoreo continuo de logs de perímetro; revisiones regulares de configuraciones de red pública; acuerdos de nivel de servicio (SLAs) con proveedores de Internet para contingencias; procedimientos de respuesta rápida ante intrusiones detectadas.*

**:white_check_mark:3.2.	Capa 2: Red Interna/Segmentación**

Medidas Técnicas

:small_blue_diamond:VLANs (Redes de Área Local Virtuales): Segmentación lógica de tráfico según funciones (NIST SP 800-207).

:small_blue_diamond:SDN (Red Definida por Software): Control programable de tráfico interno.

:small_blue_diamond:ACLs (Listas de Control de Acceso): Reglas para limitar tráfico entre segmentos.

:small_blue_diamond:NAC (Control de Acceso a la Red): Autenticación previa al acceso.
Medidas Administrativas

*Políticas de segmentación de red documentadas; clasificación de activos y asignación de niveles de confianza; análisis de flujo de red para identificar comunicaciones inusuales; pentesting interno y auditorías de configuración de switches y routers; actualización periódica de reglas de VPN y filtrado inter-sucursal. Se reduce así la capacidad de los atacantes de propagarse y filtrar datos, ya que “la segmentación de red ayuda a limitar la exposición interna […] y a contener la propagación del malware”*

**:white_check_mark:3.3.	Capa 3: Endpoint/Dispositivos**

Medidas Técnicas

:small_blue_diamond:EDR (Detección y Respuesta en el Endpoint): Amenazas en tiempo real con contención automatizada (NIST SP 800-128).

:small_blue_diamond:MDM (Gestión de Dispositivos Móviles): Control sobre configuración de equipos móviles.

:small_blue_diamond:Hardening (Endurecimiento de sistemas): Reducción de superficie de ataque según CIS Benchmarks.
Medidas Administrativas

*Políticas de uso de dispositivos (solo software autorizado, sin permisos administrativos innecesarios); gestión de inventario de hardware/software; formación a usuarios sobre buenas prácticas de seguridad (p. ej. no descargar software de fuentes no confiables); escaneo regular de vulnerabilidades en estaciones de trabajo; uso de cuentas no-administrador para tareas diarias.*

**:white_check_mark:3.4.	Capa 4: Aplicaciones**

Medidas Técnicas

:small_blue_diamond:SAST/DAST (Análisis Estático/Dinámico de Seguridad): Identificación de vulnerabilidades (NIST SP 800-218 SSDF - Marco de Desarrollo Seguro).

:small_blue_diamond:	DevSecOps (Desarrollo Seguro en DevOps): Seguridad desde la fase de diseño (ISO/IEC 27034).

:small_blue_diamond:OAuth/SAML (Protocolos de Autenticación): Federación segura de identidad.

:small_blue_diamond:Pentesting (Pruebas de Penetración): Validación de controles (OWASP ASVS - Estándar de Validación de Seguridad de Aplicaciones).
Medidas Administrativas

Ciclo de desarrollo seguro (Secure SDLC) con revisión de código y pruebas de seguridad; proceso de gestión de parches de aplicaciones; lista blanca de aplicaciones permitidas (whitelisting); revisiones de configuración de servidores de aplicaciones; políticas de gestión de cambios y control de versiones. Estas medidas previenen la explotación de fallos en el software de la empresa.

**:white_check_mark:3.5.	Capa 5: Datos**

Medidas Técnicas

:small_blue_diamond:AES (Estándar de Cifrado Avanzado): Cifrado con AES-256 y TLS (Seguridad de la Capa de Transporte) 1.3 (ISO/IEC 27040).

:small_blue_diamond:DLP (Prevención de Pérdida de Datos): Protección frente a fuga de información (NIST SP 800-111).

Medidas Administrativas
Políticas de respaldo y recuperación (evaluadas y probadas regularmente); clasificación formal de la información y manejo de datos sensibles; retención mínima de datos críticos; rotación de llaves de cifrado; registro de accesos a información crítica. Mantener redundancia de datos (almacenamiento multiregión, réplicas) incrementa la resiliencia frente a ransomware.

**:white_check_mark:3.6.	Capa 6: Identidad y Acceso**

Medidas Técnicas

:small_blue_diamond:MFA (Autenticación Multifactor): Segundo factor obligatorio (NIST SP 800-63B).

:small_blue_diamond:IAM (Gestión de Identidades y Accesos): Centralización del control de identidades.

:small_blue_diamond:SSO (Inicio de Sesión Único): Simplificación y control de autenticación.
Medidas Administrativas.

Revisión periódica de permisos (asegurando que nadie tenga accesos excesivos); políticas claras de creación y eliminación de cuentas (on/off boarding); concienciación sobre higiene de contraseñas (no compartir credenciales, uso de MFA); gestión de cuentas de servicio y de administrador separadas; capacitación en reconocimiento de ataques de ingeniería social dirigidos a robar credenciales. Según la práctica Zero Trust, “no se debe confiar por defecto en ningún usuario”

**:white_check_mark:3.7.	Capa 7: Operaciones y Concienciación**

Medidas Técnicas

:small_blue_diamond:SOC (Centro de Operaciones de Seguridad): Monitoreo y respuesta en tiempo real (NIST SP 800-137).

:small_blue_diamond:SIEM (Gestión de Eventos e Información de Seguridad): Correlación y análisis de eventos.

:small_blue_diamond:CTI (Inteligencia de Amenazas Cibernéticas): Anticipación de amenazas (STIX/TAXII - Estandarización de Intercambio de Información).
Medidas Administrativas.

Programa de entrenamiento y ejercicios de concienciación (phishing simulation, capacitación periódica); auditorías y pruebas de penetración regulares (red teams, CTF internos); plan de respuesta a incidentes y continuidad de negocio (realizar simulacros con todo el equipo); revisión constante de políticas de seguridad y cumplimiento de estándares (ISO 27001, NIST CSF); evaluación de nuevos riesgos y tecnologías emergentes mediante informes de inteligencia de amenazas y participación en comunidades de seguridad. Según diversos expertos, la mejora continua de la estrategia de defensa (incorporando lecciones de incidentes previos) es esencial

---
![Imagen de WhatsApp 2025-06-16 a las 13 36 03_830e16d6](https://github.com/user-attachments/assets/4d9ee9b8-21bc-4eb5-93fb-fd3ee8954634)

# :four:	Respuesta al Incidente (10 de junio de 2025)

**:white_check_mark:4.1.	Contención:**

:small_blue_diamond:Aislamiento de máquinas afectadas: Se realiza mediante políticas de red en switches y firewalls para cortar la conectividad de dispositivos sospechosos, utilizando capacidades NAC (Control de Acceso a la Red) y EDR (Detección y Respuesta en el Endpoint).

:small_blue_diamond:Desactivación de cuentas sospechosas: IAM (Gestión de Identidades y Accesos) se usa para suspender temporalmente usuarios comprometidos, aplicando procedimientos definidos en NIST SP 800-53 IA-5 y AC-2.

:small_blue_diamond:Bloqueo de conexiones externas: Reglas de firewall y listas negras en sistemas perimetrales (NGFW y DNS Filtering) se ajustan para cortar comunicaciones maliciosas. Conforme con NIST SP 800-61 Rev. 2 (Computer Security Incident Handling Guide).

**:white_check_mark:4.2.	Erradicación:**

:small_blue_diamond:Eliminación de malware: EDR y antivirus con capacidades heurísticas ejecutan análisis profundos y scripts de remediación. ISO/IEC 27035 establece estos pasos como parte del tratamiento de incidentes.

:small_blue_diamond:Parches de seguridad: Se aplica una actualización inmediata del sistema comprometido mediante un proceso de gestión de parches documentado (NIST SP 800-40 Rev. 3).

:small_blue_diamond:Revocación y recreación de credenciales: Uso de herramientas IAM para forzar el cambio de contraseñas e invalidar tokens activos, alineado con NIST SP 800-63B.

**:white_check_mark:4.3.	Recuperación:**

:small_blue_diamond:Restauración desde backups validados: Copias de seguridad almacenadas fuera de línea (air-gapped) se restauran según políticas BCP/DRP (NIST SP 800-34 Rev.1, ISO/IEC 27031).

:small_blue_diamond:Verificación de integridad: Se aplican hashes criptográficos (SHA-256) para validar la autenticidad de los sistemas restaurados.

:small_blue_diamond:Reintegración por etapas: Se aplica el enfoque de zonas seguras (clean zone) para reincorporar progresivamente los sistemas, priorizando servicios críticos con base en análisis de impacto al negocio (ISO/IEC 27005).

Normas: NIST SP 800-61 Rev. 2, NIST SP 800-40, NIST SP 800-63B, ISO/IEC 27035, 27031.

---
![image](https://github.com/user-attachments/assets/cdfc4bfe-0e53-44c3-a5be-1bf66f8ae269)

# :five:	Monitoreo y Mejora Continua

:red_circle:Ciclo PDCA (Planificar-Hacer-Verificar-Actuar): Aplicado mediante un programa de gestión de seguridad documentado. Se definen objetivos de control, se implementan, se auditan (internamente con ISO/IEC 27001 A.18.2.2) y se corrigen desviaciones.

:red_circle:Auditorías periódicas: Se efectúan evaluaciones técnicas y de cumplimiento trimestrales, conforme con NIST CSF (Marco de Ciberseguridad) función "Detect" y control ISO/IEC 27001 A.18.2.3.

:red_circle:Ejercicios Red/Blue Team: Simulaciones ofensivas/defensivas con reportes post mortem documentados. Alineado con NIST SP 800-115 (Technical Guide to Information Security Testing).

:red_circle:Métricas de desempeño: Uso de KPIs (Indicadores Clave de Desempeño) y KRIs (Indicadores Clave de Riesgo) para evaluar efectividad. Ej: tiempo medio de detección (MTTD), tiempo medio de respuesta (MTTR), conforme a ISO/IEC 27004.

:red_circle:Integración de CTI e IoCs: Consumo de feeds STIX/TAXII para enriquecer la detección con amenazas externas. Procesos respaldados por NIST SP 800-150 (Guide to Cyber Threat Information Sharing).

:red_circle:Entrenamiento continuo: Programas de formación periódica y simulacros de phishing refuerzan la concienciación del personal. La cultura de seguridad se fortalece con campañas internas (boletines, talleres) y recordatorios de protocolos. El factor humano es crítico en casi tres cuartas partes de los ataques, por lo que el entrenamiento debe ser recurrente y actualizado con ejemplos reales.

:red_circle:Threat Intelligence: Integrar fuentes de inteligencia sobre amenazas (por ejemplo CISA, CERTs, plataformas de inteligencia de código abierto) en el SOC/SIEM para ajustar defensas según actores conocidos. Analizar patrones de ataques recientes (e.g. campañas de ransomware) ayuda a actualizar firmas y políticas (IPS, EDR, filtros de correo)

*Normas: NIST CSF, ISO/IEC 27004, ISO/IEC 27001 A.18, NIST SP 800-115, NIST SP 800-150.*

---

# :orange_book::closed_book::green_book:Bibliografía Normativa Utilizada::computer::smiling_imp::neckbeard:

•	NIST SP 800 Series (30, 40, 53, 61, 63, 92, 111, 115, 137, 150, 207, 218, 34).

•	ISO/IEC 27000 Series (27001, 27002, 27004, 27005, 27031, 27035, 27040).

•	CIS Controls v8.

•	OWASP Top 10, ASVS, SSDF.

•	MITRE ATT&CK Framework.

**Este plan técnico integral fortalece la postura de ciberresiliencia de TechSolutions Corp. mediante la implementación estructurada de controles de defensa en profundidad con base en estándares internacionales y mejores prácticas de la industria.**

