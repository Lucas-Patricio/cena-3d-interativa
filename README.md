# 🌲 Three.js · Forest Road Viewer

Atividade prática de computação gráfica — cena 3D interativa utilizando **Three.js r128**, com modelo carregado do Sketchfab via **GLTFLoader**, câmera manipulável com **OrbitControls** e modo de exploração em primeira pessoa com **PointerLockControls**.

---

## 📦 Modelo utilizado

| Campo | Dados |
|-------|-------|
| **Nome** | veículo_explorer |
| **Autor** | Leandro.Gomes |
| **Licença** | CC Attribution (CC BY 4.0) |
| **Link** | https://sketchfab.com/3d-models/veiculo-explorer-7c797ab552f14393859e9ab89d798dd9 |
| **Formato** | GLB |
| **Triângulos** | 15.2k |

O arquivo `scene.glb` já está incluído na pasta `models/` deste repositório — não é necessário baixar nada.

---

## 🚀 Como executar

Como o modelo já está no repositório, basta clonar e subir um servidor local:

```bash
git clone https://github.com/Lucas-Patricio/cena-3d-interativa.git
cd cena-3d-interativa
npx serve .
```

Acesse `http://localhost:3000` no navegador.

> **Por que não funciona com duplo clique no index.html?**
> O GLTFLoader faz requisições HTTP para carregar o modelo. Navegadores bloqueiam requisições `file://` por segurança — um servidor HTTP resolve isso.

Alternativas ao `npx serve`:
```bash
# Python 3
python3 -m http.server 8080

# Node http-server
npx http-server .
```

---

## 🗂️ Estrutura do projeto

```
cena-3d-interativa/
├── index.html        # Cena Three.js completa
├── models/
│   └── scene.glb     # Modelo 3D (veículo_explorer por Leandro.Gomes)
└── README.md
```

---

## ✅ Critérios implementados

| Critério | Implementação |
|----------|--------------|
| **Modelo Sketchfab via GLTFLoader** | `THREE.GLTFLoader` carrega `models/scene.glb`; centralização e escala automáticas via `Box3` |
| **OrbitControls** (rotação, zoom, pan) | `THREE.OrbitControls` com damping, limites de distância e suporte a touch |
| **Luz direcional + luz ambiente** | `DirectionalLight` (sol) com shadow map 4096×4096 + `AmbientLight` + `HemisphereLight` (céu/chão) + luz de bounce |
| **Loop com requestAnimationFrame** | Função `animationLoop()` recursiva, atualiza controls e renderiza a cena a cada frame |
| **Resize handler** | `window.addEventListener('resize', ...)` atualiza `camera.aspect`, `updateProjectionMatrix()` e `renderer.setSize()` |
| **Código legível** | Objeto `CONFIG` centralizado, comentários em PT-BR, nomes descritivos, sem código morto |

---

## 🌲 Cena — Estrada na Floresta

O modelo é posicionado sobre uma estrada de asfalto com:

- **Chão** de grama e asfalto com acostamento de terra
- **Faixas tracejadas** amarelas no centro da pista
- **24 árvores procedurais** distribuídas dos dois lados
- **Névoa exponencial** (`FogExp2`) que dissolve as árvores ao fundo
- **Céu azul de dia** como background da cena
- **Sol** (`DirectionalLight`) posicionado alto com sombras suaves na estrada
- **HemisphereLight** simulando luz do céu (azul) + reflexo do chão verde
- **EnvMap** via `PMREMGenerator` — reflexo do céu e da floresta na lataria do veículo

---

## 🎮 Controles

### Modo Órbita (padrão)

| Ação | Mouse | Touch |
|------|-------|-------|
| Rotacionar | Botão esquerdo + arrastar | 1 dedo |
| Zoom | Scroll | Pinça (2 dedos) |
| Pan | Botão direito + arrastar | 2 dedos deslizando |

### Modo FPS (pressione **F** ou clique no botão)

| Tecla | Ação |
|-------|------|
| W / A / S / D | Mover câmera |
| Mouse | Olhar ao redor |
| ESC | Liberar mouse |
| F | Voltar ao modo órbita |

---

## 🛠️ Tecnologias

- [Three.js r128](https://threejs.org/) — via CDN
- `THREE.GLTFLoader` — carregamento de modelos GLTF/GLB
- `THREE.OrbitControls` — controle de câmera por órbita
- `THREE.PointerLockControls` — navegação em primeira pessoa (FPS)
- `THREE.PMREMGenerator` — geração de envMap para reflexos PBR
- HTML5 + CSS3 (sem frameworks)

---

## 📄 Licença

Código-fonte: MIT
Modelo 3D: CC Attribution — [veículo_explorer por Leandro.Gomes](https://sketchfab.com/3d-models/veiculo-explorer-7c797ab552f14393859e9ab89d798dd9)
