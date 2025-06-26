# Resumen

Como parte del entrenamiento en MuleSoft, desarrollé una solución que permite exponer datos de clientes almacenados en una base de datos **MySQL** mediante una **API**. Esta solución tiene como objetivo facilitar al equipo de **marketing** el acceso a datos.
(Descargar archivo de Documentación)
---

## ✅ Requisitos Implementados

- **Ruta de exposición:**  
  La API expone los datos de clientes a través de la ruta:  
  `/api/v1/sps/customers`

- **Gestión de entornos:**  
  Se crearon dos archivos de propiedades:  
  - Uno para entorno **local**  
  - Otro para entorno de **desarrollo (dev)**

- **Organización del proyecto:**  
  La solución está estructurada en dos archivos principales:  
  - Uno para la **implementación lógica**  
  - Otro para los **componentes globales**

- **Seguridad:**  
  Las credenciales de conexión a la base de datos están protegidas utilizando **Secure Properties**

- **Diseño de la API:**  
  Se construyó la **especificación de la API (RAML)**

- **Despliegue:**  
  La aplicación fue desplegada correctamente en **CloudHub**

---

## 🌟 Extras Implementados

1. Publicación de la API en **API Manager**
2. Configuración de **API Autodiscovery** en la aplicación para su administración desde API Manager
3. Aplicación de la política de seguridad **Client ID Enforcement** para controlar el acceso a la API

---

## 🔍 Exploración Adicional

Además de los puntos requeridos y los extras, realicé una **exploración adicional** sobre **autenticación mediante JWT Validation**, configurando esta política en API Manager para comprender cómo implementar en MuleSoft otras formas de **control de acceso y seguridad**.

---

## 📈 Resultados

**Priscila Martinez**

> **Nota:** Esta sección fue hecha con la finalidad de demostrar el funcionamiento. En el PDF de Documentación, en el apartado de *Desarrollo de Práctica*, estará descrito el procedimiento, análisis y aprendizaje.

---

### 🔗 API desplegada en CloudHub

**URL:**  
[https://sps-customers-e96hyd.5sc6y6-2.usa-e2.cloudhub.io/api/v1/sps/customers](https://sps-customers-e96hyd.5sc6y6-2.usa-e2.cloudhub.io/api/v1/sps/customers)

---

### 🔐 Parámetros requeridos por el Client ID Enforcement
client_id: cbca3d1cce834f2abf45364d216862fa
client_secret: 40EC2EA4Fb6e40c2a0cd553393aa8e89


## 🛡️ Especificación del JWT

Para poder generar un token válido, es imprescindible que este contenga la clave `"role"` con el valor `"marketing"`, ya que la validación configurada en **API Manager → Policy → JWT Validation** permite el acceso al recurso (`GET` para obtener clientes) únicamente a aquellos usuarios cuyo rol sea de marketing.

Además, es fundamental que el valor de expiración (`exp`) del token no haya caducado, ya que también se valida este parámetro.

Para facilitar la prueba, se sugiere copiar y pegar el token resaltado en amarillo, el cual cumple con todos los requisitos mencionados y con las especificaciones del JWT.

### Header: Algorithm & Token Type

{
  "alg": "HS256",
  "typ": "JWT"
}

### Payload
{
"sub": "1234567890", 
"name": "PriscilaM", 
"role": "marketing", 
"exp": 4102444800
}

### Sign JWT: Secret
a-string-secret-at-least-256-bits-long 

### TOKEN
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IlByaXNjaWxhTSIsInJvbGUiOiJtYXJrZXR
 pbmciLCJleHAiOjQxMDI0NDQ4MDB9.F1rU9Ghm2JXgDru3YfsG5V-HSeTNOiTDi_R7TwfxdpU 



## 📈 PROBAR EN CURL - WINDOWS POWERSHELL
curl.exe -u cbca3d1cce834f2abf45364d216862fa:40EC2EA4Fb6e40c2a0cd553393aa8e89 -H "x-access-token: 
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IlByaXNjaWxhTSIsInJvbGUiOi
 JtYXJrZXRpbmciLCJleHAiOjQxMDI0NDQ4MDB9.F1rU9Ghm2JXgDru3YfsG5V-HSeTNOiTDi_R7TwfxdpU" -X GET 
"https://sps-customers-e96hyd.5sc6y6-2.usa-e2.cloudhub.io/api/v1/sps/customers" 
