# 🛠️ Configuración de Jenkins paso a paso después del `docker compose up`

## ✅ 1. Verifica que Jenkins está corriendo

```bash
docker ps
```

Debe aparecer algo como:

```
CONTAINER ID   IMAGE                ...   PORTS
abcd1234       jenkins/jenkins:lts  ...   0.0.0.0:8080->8080/tcp
```

Accede desde tu navegador:
📍 [http://localhost:8080](http://localhost:8080)

---

## 🔑 2. Obtener la contraseña inicial

Jenkins genera un password temporal al iniciarse por primera vez. Para verlo, ejecuta:

```bash
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

📋 Copia ese password y pégalo en el navegador cuando Jenkins lo solicite.

---

## 🧩 3. Instalar los plugins recomendados

- Jenkins te preguntará si quieres instalar plugins recomendados: **haz clic en “Install suggested plugins”**.
- Espera a que finalice la instalación.

---

## 👤 4. Crea el usuario administrador

Rellena el formulario:

- **Nombre de usuario:** admin (o el que prefieras)
- **Contraseña:** \*\*\*\*\*\*\*\*
- **Nombre completo:** Brayan (o tu nombre)
- **Correo electrónico:** [tuemail@dominio.com](mailto:tuemail@dominio.com)

Haz clic en **Save and Continue**.

---

## 🌐 5. Configura la URL de Jenkins

Cuando Jenkins te pregunte por la URL, deja el valor por defecto o pon:

```
http://localhost:8080/
```

Haz clic en **Save and Finish**.

---

## 🎉 6. Jenkins está listo

Verás el botón:

```
Start using Jenkins
```

Haz clic para entrar al panel principal.

---

## 🧰 7. Instalar los plugins adicionales necesarios

Desde el panel principal:

```
Manage Jenkins → Manage Plugins → Available
```

🔍 Busca e instala los siguientes plugins:

- **Maven Integration**
- **SonarQube Scanner**
- (opcional) **Docker Pipeline**

---

## 🧪 8. Configurar herramientas globales

Desde el panel:

```
Manage Jenkins → Global Tool Configuration
```

## 📦 Java

- **Name:** `Java21`
- **JAVA_HOME:** `/opt/java/openjdk`
  _(o la ruta exacta que obtuviste con `readlink -f $(which java)` dentro del contenedor)_

---

## 🧰 Maven

- **Name:** `Maven3`
- **MAVEN_HOME:** `/usr/share/maven`
  _(verificado con `mvn -v`)_

---

## 🔍 SonarQube

- Ir a `Manage Jenkins → Configure System`
- Buscar la sección **SonarQube Servers**
- Haz clic en **Add SonarQube**

  - **Name:** `SonarQube`
  - **Server URL:** `http://sonarqube:9000`
  - **Authentication Token:** el token que generaste en `http://localhost:9000` → `My Account` → `Security`
