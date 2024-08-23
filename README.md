# 🔐 JWT Algorithms: HS256 vs RS256

Cuando se trabaja con JSON Web Tokens (JWT), elegir el algoritmo adecuado para firmar y validar los tokens es crucial para la seguridad y la arquitectura de tu aplicación. Los dos algoritmos más comunes son `HS256` y `RS256`, cada uno con sus propias características y casos de uso.

## ⚙️ HS256 (HMAC con SHA-256)

- **Tipo de cifrado:** Simétrico (una misma clave secreta se usa tanto para firmar como para verificar el token).
- **Casos de uso comunes:**
  - Aplicaciones donde tanto la generación como la validación del token se realizan en el mismo entorno o por el mismo servicio.
  - Entornos donde es posible mantener segura la clave secreta en todas las partes que necesitan generar o validar tokens.
- **Ventajas:**
  - Menor complejidad porque solo se maneja una clave secreta.
  - Desempeño rápido debido a que el algoritmo es menos complejo.
- **Desventajas:**
  - La seguridad depende de la protección de la clave secreta, que debe compartirse con cualquier servicio que necesite verificar el token. Si la clave es comprometida, toda la seguridad del sistema se ve afectada.

## 🔑 RS256 (RSA con SHA-256)

- **Tipo de cifrado:** Asimétrico (se usan claves diferentes para firmar y verificar el token: una clave privada para firmar y una clave pública para verificar).
- **Casos de uso comunes:**
  - Aplicaciones distribuidas donde varios servicios necesitan verificar el token, pero solo uno debe tener acceso a la clave privada para firmar tokens (por ejemplo, sistemas de microservicios).
  - Escenarios donde la seguridad es crítica y se prefiere no compartir la clave privada.
- **Ventajas:**
  - Mayor seguridad porque solo la clave pública se distribuye a los servicios que necesitan validar el token. La clave privada permanece segura y solo es conocida por el servicio que genera los tokens.
  - Adecuado para arquitecturas distribuidas donde múltiples servicios de confianza necesitan validar tokens.
- **Desventajas:**
  - Mayor complejidad en la gestión de claves (clave pública y privada).
  - Un poco más lento en términos de rendimiento debido a la criptografía asimétrica.

## 📌 ¿Cuándo usar uno u otro?

- **Usa HS256 si:** 
  - Controlas tanto la emisión como la validación de los tokens dentro de un mismo servicio o sistema y puedes garantizar la seguridad de la clave secreta.
  - Quieres un enfoque más simple y de menor carga computacional.
  
- **Usa RS256 si:**
  - Necesitas compartir la validación del token entre múltiples servicios, pero no quieres compartir la clave privada.
  - Quieres mejorar la seguridad separando la generación de tokens (clave privada) y la validación (clave pública).

### 📝 Resumen

`HS256` es adecuado para sistemas más simples y controlados, mientras que `RS256` es mejor para arquitecturas distribuidas y aplicaciones donde la seguridad es primordial.
