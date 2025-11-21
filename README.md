# AWS Base de Datos – DynamoDB & S3

Este repositorio contiene la configuración inicial para una base de datos sencilla utilizando **AWS DynamoDB** y **Amazon S3**, ideal para proyectos pequeños como aplicaciones móviles, mini–redes sociales o prototipos serverless.

---

## 📁 Estructura del Repositorio

```
/
├── DynamoDB/
│   └── tabla-posts.json
├── s3/
│   └── bucket-policy.json
└── README.md
```

---

## 🗄️ DynamoDB – Tabla **Posts**

La carpeta `DynamoDB/` contiene la definición de la tabla utilizada para almacenar publicaciones.

### 📌 Esquema de la tabla

```json
{
  "TableName": "Posts",
  "AttributeDefinitions": [
    {
      "AttributeName": "postId",
      "AttributeType": "S"
    }
  ],
  "KeySchema": [
    {
      "AttributeName": "postId",
      "KeyType": "HASH"
    }
  ],
  "BillingMode": "PAY_PER_REQUEST"
}
```

### ✔️ Detalles importantes

- **Llave primaria:** `postId` (tipo `String`)
- **Sin índices secundarios** — estructura simple
- **BillingMode:** `PAY_PER_REQUEST`, ideal para uso ligero o intermitente
- No requiere capacidad provisionada ni ajustes adicionales.

---

## 🖼️ S3 – Bucket de Imágenes

El bucket `mini-instagram-posts` se usa para almacenar archivos multimedia de las publicaciones.

### 📌 Política del bucket

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mini-instagram-posts/*"
    }
  ]
}
```

### ✔️ ¿Qué permite esta política?

- Permite acceso **público de solo lectura** a todos los objetos dentro del bucket.
- Es ideal para aplicaciones donde las imágenes deben ser visibles por cualquier usuario.
- ⚠️ **Advertencia:** no es apropiado para datos privados o información sensible.

---

## 🚀 Cómo usar este repositorio

### 1️⃣ Crear la tabla en DynamoDB

Puedes usar AWS CLI:

```bash
aws dynamodb create-table --cli-input-json file://DynamoDB/tabla-posts.json
```

---

### 2️⃣ Crear el bucket S3 y aplicar la política

```bash
aws s3api create-bucket --bucket mini-instagram-posts --region us-east-1
aws s3api put-bucket-policy --bucket mini-instagram-posts --policy file://s3/bucket-policy.json
```

---

## 🧩 Ideal para proyectos como:

- Apps tipo Instagram
- Portafolios con imágenes dinámicas
- Pruebas de arquitectura serverless
- Proyectos educativos

---
