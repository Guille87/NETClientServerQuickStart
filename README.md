## Scripts

### HelloWorldManager.cs
- **Variables**:
    - `private static NetworkManager m_NetworkManager` → Referencia al NetworkManager, gestiona la conexión de red y el estado del servidor/cliente.
- **Métodos**:
    - `Awake()` → Obtiene la referencia al `NetworkManager`.
    - `OnGUI()` → Dibuja la interfaz gráfica.
    - `StartButtons()` → Permite iniciar el juego como Host, Cliente o Servidor.
    - `StatusLabels()` → Muestra información sobre el estado de la red.
    - `SubmitNewPosition()` → Permite cambiar la posición del jugador.

### HelloWorldPlayer.cs
- **Variables**:
    - `public NetworkVariable<Vector3> Position` → Almacena y sincroniza la posición de los jugadores en la red.
- **Métodos**:
    - `OnNetworkSpawn()` → Se ejecuta al conectarse a la red; si el jugador es el dueño `(IsOWner)`, se mueve a una nueva posición aleatoria en el servidor.
    - `Move()` → Solicita un cambio de posición.
    - `SubmitPositionRequestRpc(RpcParams rpcParams = default)` → RPC que mueve al jugador a una nueva posición aleatoria en el servidor.
    - `GetRandomPositionOnPlane()` → Genera una posición aleatoria en un plano.
    - `Update()` → Sincroniza la posición del jugador con la variable de red.

### NetworkTransformTest.cs
- **Métodos**:
    - `Update()` → Calcula una nueva posición en un círculo y la actualiza en el servidor.

### RPCTest.cs
- **Métodos**:
    - `OnNetworkSpawn()` → Si el objeto no es servidor pero es dueño, envía un RPC al servidor.
    - `ClientAndHostRpc(int value, ulong sourceNetworkObjectId)` → Envía un RPC al cliente y al host, si el objeto de red es propietario, llama al método ServerOnlyRpc.
    - `ServerOnlyRpc(int value, ulong sourceNetworkObjectId)` → Envía un RPC al servidor, que responde con un RPC a todos los clientes.

## Componentes del GameObject `NetworkManager`
### Network Manager
- Gestiona la comunicación entre clientes y el servidor.
- Sincroniza objetos en la red.
### Unity Transport
- Transporta datos para enviar y recibir paquetes de red.
### HelloWorld Manager
- Se encarga de manejar la interfaz gráfica y la conexión del juego.

## Componentes del Prefab `Player`
### Network Object
- Permite que el objeto sea reconocido y gestionado por la red.
### HelloWorld Player
- Maneja el movimiento del jugador en red.
### Rpc Test
- Asegura que las acciones del jugador se sincronicen correctamente entre los diferentes clientes.
### Network Transform
- Sincroniza la posición, rotación y escala del jugador en la red.