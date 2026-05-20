# 🌲 Three.js · Forest Road Viewer

Atividade prática de computação gráfica — cena 3D interativa utilizando **Three.js r128**, com modelo carregado do Sketchfab via **GLTFLoader**, câmera manipulável com **OrbitControls** e modo de exploração em primeira pessoa com **PointerLockControls**.

---

## 📦 Modelo utilizado

| Campo | Dados |
|-------|-------|
| **Nome** | Vintage Radio |
| **Autor** | Sketchfab Community |
| **Licença** | CC Attribution (CC BY 4.0) |
| **Link** | [https://sketchfab.com/3d-models/vintage-radio-ffe54f9374ae4a8c9b0e5d39c0ddbbb5](https://sketchfab.com/3d-models/veiculo-explorer-7c797ab552f14393859e9ab89d798dd9) |
| **Formato** | glTF / GLB |

> ⚠️ O modelo **não está incluído** no repositório por questões de tamanho de arquivo.  
> Siga as instruções abaixo para configurar o projeto localmente.

---

## 🚀 Como executar

### 1. Baixar o modelo do Sketchfab

1. Acesse o link do modelo acima
2. Clique em **Download 3D Model**
3. Selecione o formato **GLB** (preferível) ou **glTF**
4. Coloque o arquivo `scene.glb` (ou renomeie para `scene.glb`) dentro da pasta `models/`

### 2. Servir localmente (obrigatório — CORS)

```bash
# Opção A — npx serve (recomendado)
npx serve .

# Opção B — Python 3
python3 -m http.server 8080

# Opção C — Node.js http-server
npx http-server .
```

Acesse `http://localhost:3000` (ou a porta exibida no terminal).

---

## 🗂️ Estrutura do projeto

```
threejs-sketchfab/
├── index.html        # Cena Three.js completa
├── models/           # Coloque aqui o scene.glb baixado do Sketchfab
│   └── scene.glb     # ← arquivo a ser adicionado manualmente
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
- **24 árvores procedurais** (tronco + três cones de copa) distribuídas dos dois lados
- **Névoa exponencial** (`FogExp2`) que dissolve as árvores ao fundo
- **Céu azul de dia** como background da cena
- **Sol** (`DirectionalLight`) posicionado alto com sombras suaves na estrada
- **HemisphereLight** simulando luz do céu (azul) + reflexo do chão verde
- **EnvMap** gerado via `PMREMGenerator` com cores de dia — reflexo do céu e da floresta aparece na lataria do modelo

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
Modelo 3D: CC Attribution — veja link do Sketchfab acima
