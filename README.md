# 🎙️ Three.js · Sketchfab Viewer

Atividade prática de computação gráfica — cena 3D interativa utilizando **Three.js r128**, com modelo carregado do Sketchfab via **GLTFLoader** e câmera manipulável com **OrbitControls**.

---

## 📦 Modelo utilizado

| Campo | Dados |
|-------|-------|
| **Nome** | Vintage Radio |
| **Autor** | Sketchfab Community |
| **Licença** | CC Attribution (CC BY 4.0) |
| **Link** | https://sketchfab.com/3d-models/vintage-radio-fa870d0b29784e29b5b95d9ee58f48ec |
| **Formato** | glTF / GLB |

> ⚠️ O modelo **não está incluído** no repositório por questões de tamanho de arquivo.  
> Siga as instruções abaixo para configurar o projeto localmente.

---

## 🚀 Como executar

### 1. Baixar o modelo do Sketchfab

1. Acesse o link do modelo acima
2. Clique em **Download 3D Model**
3. Selecione o formato **glTF** (preferível) ou **GLB**
4. Extraia o arquivo e copie `scene.glb` (ou `scene.gltf` + arquivos de suporte) para a pasta `models/` deste projeto

### 2. Servir localmente (obrigatório por conta do CORS)

Escolha uma das opções:

```bash
# Opção A — npx serve (recomendado, sem instalação prévia)
npx serve .

# Opção B — Python 3
python3 -m http.server 8080

# Opção C — Node.js http-server
npx http-server .
```

Então acesse `http://localhost:3000` (ou a porta exibida no terminal).

> **Por que não funciona com duplo clique no index.html?**  
> O GLTFLoader faz requisições HTTP para carregar o modelo. Navegadores bloqueiam requisições de arquivos locais (`file://`) por segurança — um servidor HTTP resolve isso.

---

## 🗂️ Estrutura do projeto

```
threejs-sketchfab/
├── index.html        # Cena Three.js completa (renderer, câmera, luzes, controls, loop)
├── models/           # Coloque aqui o scene.glb baixado do Sketchfab
│   └── scene.glb     # ← arquivo a ser adicionado manualmente
└── README.md
```

---

## ✅ Critérios implementados

| Critério | Implementação |
|----------|--------------|
| **Modelo Sketchfab via GLTFLoader** | `THREE.GLTFLoader` carrega `models/scene.glb`; centralização e escala automáticas via BoundingBox |
| **OrbitControls** (rotação, zoom, pan) | `THREE.OrbitControls` com damping, limites de distância e suporte a touch |
| **Luz direcional + luz ambiente** | `AmbientLight` (cor azulada, 0.6), `DirectionalLight` principal (0xffeedd, 1.8) com shadow map 2048×2048, mais `DirectionalLight` de preenchimento (fill) |
| **Loop com requestAnimationFrame** | Função `animationLoop()` chama `requestAnimationFrame` recursivamente, atualiza controls e renderiza a cena |
| **Resize handler** | `window.addEventListener('resize', onWindowResize)` atualiza `camera.aspect`, `camera.updateProjectionMatrix()` e `renderer.setSize()` |
| **Código legível** | Variáveis descritivas em inglês/português, objeto `CONFIG` centralizado, comentários em PT-BR, sem código morto |

---

## 🎮 Controles de câmera

| Ação | Mouse | Touch |
|------|-------|-------|
| Rotacionar | Botão esquerdo + arrastar | 1 dedo |
| Zoom | Scroll / roda do mouse | Pinça (2 dedos) |
| Pan | Botão direito + arrastar | 2 dedos deslizando |

---

## 🛠️ Tecnologias

- [Three.js r128](https://threejs.org/) — via CDN (cdnjs.cloudflare.com)
- `THREE.GLTFLoader` — carregamento de modelos GLTF/GLB
- `THREE.OrbitControls` — controle de câmera interativo
- `THREE.WebGLRenderer` — renderização WebGL 2 com sRGB encoding e tonemapping ACES Filmic
- HTML5 + CSS3 (sem frameworks)

---

## 📸 Features visuais

- **Tonemapping ACES Filmic** para cores mais realistas
- **Shadow maps** PCF Soft (2048×2048)
- **Auto-rotate** que pausa ao interagir
- **FPS counter** e contador de triângulos em tempo real
- **Fog** sutil para profundidade
- **Pixel ratio** adaptável (máx 2×) para telas de alta resolução
- Interface responsiva com painel de controles e barra de informações

---

## 📄 Licença

Código-fonte: MIT  
Modelo 3D: CC Attribution — veja link do Sketchfab acima
