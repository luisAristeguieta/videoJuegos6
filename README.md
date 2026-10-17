# Taller 7: Sistema de Ataque y Derrota del Enemigo

> **Aviso Académico:** Este proyecto ha sido desarrollado exclusivamente con fines formativos y académicos dentro del curso de Diseño y Desarrollo de Videojuegos 2D. Todos los recursos empleados se utilizan con propósito educativo.

Proyecto desarrollado en Unity 2D (Unity 6). En este taller se implementa el sistema de combate cuerpo a cuerpo (*melee*) para el personaje principal mediante animaciones por *Trigger*, zonas de impacto física (*Hitbox*) calculadas con `Physics2D.OverlapCircleAll`, y la destrucción autónoma del enemigo al quedarse sin puntos de salud.

---

## 📹 Video de Demostración
- **Video en Google Drive:** [Taller_7.mp4 - Google Drive](https://drive.google.com/file/d/1I-I0RkEGU089Fq45jwiEXolfpd8hj9FW/view?usp=sharing)  

---

## 🖼️ Evidencias del Proyecto

### 1. Configuración del Enemigo (Layer, BoxCollider2D y Script EnemyHealth)
Asignación de la capa `Enemy Layer`, configuración de `BoxCollider2D` y vinculación del script `EnemyHealth.cs` con salud máxima de 3:
![Enemy with Layer and Script](Entregables/Taller%207/Enemy%20with%20Layer%20and%20Script.png)

### 2. Configuración del Jugador (AttackPoint, Gizmos y Script PlayerAttack)
Objeto hijo `AttackPoint` posicionado al frente de la espada, visualización de rango (*Hitbox*) con Gizmos y vinculación de `PlayerAttack.cs`:
![Player con Script Player Attack](Entregables/Taller%207/Player%20con%20Script%20Player%20Attack.png)

---

## 🚀 Características Implementadas

1. **Configuración de Animaciones de Combate (`Animator`):**
   - Creación del parámetro de tipo *Trigger* llamado `Attack` en la ventana Animator.
   - Transición directa desde `Any State` hacia la animación `Attack` desmarcando la opción *Has Exit Time*.
   - Transición de retorno desde `Attack` hacia `Idle` con *Has Exit Time* activado y fijando `Exit Time = 1` (con duración de transición en 0), permitiendo la reproducción fluida y completa del espadazo.

2. **Marcador de Ataque y Zona de Impacto (`Hitbox`):**
   - Creación de un GameObject vacío hijo del personaje llamado `AttackPoint`, ubicado frontalmente en la posición del arma.
   - Detección precisa de enemigos en tiempo real mediante `Physics2D.OverlapCircleAll(attackPoint.position, attackRange, enemyLayer)`.
   - Incorporación de `OnDrawGizmosSelected` para visualizar el radio del ataque en color rojo directamente en la escena.

3. **Lógica de Salud y Destrucción del Enemigo (`EnemyHealth.cs`):**
   - Inicialización de salud con `maxHealth = 3` y control en `currentHealth`.
   - Método `TakeDamage(int damageAmount)` que descuenta el daño recibido.
   - Evaluación condicional `currentHealth <= 0` que dispara de forma autónoma la función `Die()`, destruyendo el GameObject con `Destroy(gameObject)`.

4. **Lógica de Ataque del Jugador (`PlayerAttack.cs`):**
   - Detección de pulsación de la tecla `Z` o clic izquierdo del ratón (`Input.GetMouseButtonDown(0)`).
   - Activación inmediata del trigger de animación `animator.SetTrigger("Attack")`.
   - Filtrado exclusivo por capa de enemigos (`enemyLayer`), localizando el componente `EnemyHealth` de cada entidad alcanzada para aplicarle el daño configurado.

5. **Configuración de Capas e Inspector:**
   - Creación y asignación de la capa `Enemy Layer` en el prefab del enemigo patrullero.
   - Vinculación en el Inspector del `Player` de las referencias `AttackPoint`, `Attack Range` (0.8) y la máscara de capa `Enemy Layer`.

---

## 📂 Estructura del Repositorio

El proyecto incluye las carpetas requeridas para abrirse directamente en Unity sin pérdida de referencias:

```text
├── Assets/                 # Carpeta completa de assets y sus archivos .meta
│   ├── Animations/
│   │   ├── Attack.anim
│   │   ├── Player.controller
│   │   └── ...
│   ├── Prefabs/
│   │   ├── Coin.prefab
│   │   └── Enemigo_Patrulla.prefab
│   ├── Scenes/
│   │   └── Level 1.unity
│   ├── Script/
│   │   ├── CameraFollow.cs
│   │   ├── Coin.cs
│   │   ├── CoinUI.cs
│   │   ├── EnemyHealth.cs
│   │   ├── EnemyPatrol.cs
│   │   ├── PlayerAttack.cs
│   │   ├── PlayerController.cs
│   │   └── PlayerHealth.cs
│   └── Sprites/
│       ├── Attack.png
│       └── ...
├── ProjectSettings/         # Configuración global del motor (Tags, Layers, Input, etc.)
├── Entregables/             # Capturas de evidencia organizadas por taller
│   ├── Taller 7/
│   │   ├── Enemy with Layer and Script.png
│   │   └── Player con Script Player Attack.png
│   └── ...
├── .gitignore               # Filtro para omitir archivos temporales y carpetas pesadas (Library, Temp, obj, etc.)
└── README.md


🛠️ Cómo Abrir el Proyecto en Unity

1. Clona este repositorio o descarga el archivo ZIP:

git clone [https://github.com/luisAristeguieta/Scrip_Animation.git](https://github.com/luisAristeguieta/Scrip_Animation.git)

2. Abre Unity Hub.
3. Haz clic en Add > Add project from disk.
4. Selecciona la carpeta raíz del repositorio clonado.
5. Abre el proyecto con Unity 6 (o versión compatible).
6. Dirígete a Assets/Scenes/ y abre la escena principal Level 1.unity.
7. Presiona Play para interactuar con el nivel y probar la recolección de monedas.
