# 🥠 Biscoito da Sorte - Vue.js

Uma aplicação web interativa de biscoito da sorte desenvolvida com Vue.js 3, HTML5, CSS3 e SVG. O usuário pode clicar no biscoito para "quebrá-lo" e revelar mensagens inspiradoras de sorte.

## 🎯 Demonstração

![Biscoito da Sorte](https://img.shields.io/badge/Status-Funcionando-brightgreen)

- **Interação:** Clique no biscoito dourado para revelar sua sorte
- **Animações:** Efeitos visuais suaves e transições elegantes  
- **Responsivo:** Funciona perfeitamente em desktop e mobile

## 🚀 Tecnologias Utilizadas

- **Vue.js 3** - Framework JavaScript reativo
- **HTML5** - estrutura semântica
- **CSS3** - Estilos avançados com animações
- **SVG** - Gráficos vetoriais para o biscoito
- **JavaScript ES6+** - Lógica da aplicação

## 📁 Estrutura do Projeto

```
biscoito-da-sorte/
├── index.html          # Arquivo HTML principal
├── style.css           # Estilos CSS separados
└── README.md           # Documentação do projeto
```

## 🔧 Instalação e Uso

### Pré-requisitos
- Navegador web moderno (Chrome, Firefox, Safari, Edge)
- Não requer instalação de dependências

### Como executar
1. **Clone ou baixe os arquivos**
2. **Certifique-se que ambos os arquivos estão na mesma pasta:**
   - `index.html`
   - `style.css`
3. **Abra o arquivo `index.html` no navegador**
4. **Pronto! O biscoito da sorte está funcionando** 🎉

## 💻 Explicação do Código

### 📄 HTML (index.html)

#### Estrutura Principal
```html
<div id="app">
    <!-- Partículas animadas de fundo -->
    <div class="particulas">...</div>
    
    <div class="container">
        <!-- Título principal -->
        <h1>🥠 Biscoito da Sorte</h1>
        
        <!-- Instruções para o usuário -->
        <div class="instrucao">...</div>
        
        <!-- Container do biscoito SVG -->
        <div class="biscoito-container">...</div>
        
        <!-- Container da mensagem -->
        <div class="mensagem-container">...</div>
        
        <!-- Botão para novo biscoito -->
        <button class="botao">...</button>
    </div>
</div>
```

#### SVG do Biscoito
O biscoito é criado usando SVG (Scalable Vector Graphics) com duas versões:

**Biscoito Fechado:**
```html
<ellipse cx="100" cy="100" rx="80" ry="60" fill="url(#biscoitoGradient)"/>
<path d="M 40 100 Q 100 60 160 100 Q 100 140 40 100" fill="url(#biscoitoGradient)"/>
```

**Biscoito Quebrado:**
```html
<path d="M 30 100 Q 70 70 90 100 L 85 120 Q 60 130 30 100"/>
<path d="M 110 100 Q 140 70 170 100 Q 150 130 120 120 L 110 100"/>
<rect x="85" y="95" width="30" height="10" fill="white"/> <!-- Papel da sorte -->
```

### 🎨 CSS (style.css)

#### Reset e Layout Base
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

#### Animações Principais

**Efeito Glow no Título:**
```css
@keyframes glow {
    from { text-shadow: 2px 2px 4px rgba(0,0,0,0.3); }
    to { text-shadow: 2px 2px 20px rgba(255,255,255,0.5); }
}
```

**Animação de Entrada da Mensagem:**
```css
@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
```

**Efeito Shimmer na Mensagem:**
```css
.mensagem::before {
    content: '';
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
    animation: shimmer 2s infinite;
}
```

**Partículas Flutuantes:**
```css
@keyframes flutuar {
    0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
    100% { transform: translateY(-100px) rotate(360deg); opacity: 0; }
}
```

#### Estados do Biscoito
```css
.biscoito:hover {
    transform: scale(1.1) rotateY(15deg);
    filter: brightness(1.2);
}

.biscoito.quebrado {
    transform: scale(0.8) rotateY(180deg);
    opacity: 0.7;
}
```

### ⚡ JavaScript (Vue.js)

#### Configuração da Aplicação Vue
```javascript
const { createApp } = Vue;

createApp({
    data() {
        return {
            mensagemRevelada: false,    // Controla se a mensagem foi revelada
            mensagemAtual: '',          // Armazena a mensagem atual
            mensagens: [...]            // Array com 25 mensagens de sorte
        }
    },
    methods: {
        quebrarBiscoito() {
            if (!this.mensagemRevelada) {
                this.mensagemRevelada = true;
                this.mensagemAtual = this.mensagens[Math.floor(Math.random() * this.mensagens.length)];
            }
        },
        novoBiscoito() {
            this.mensagemRevelada = false;
            this.mensagemAtual = '';
        }
    }
}).mount('#app');
```

#### Funcionalidades Vue.js Utilizadas

**Reatividade:**
- `mensagemRevelada`: Controla a exibição condicional
- `mensagemAtual`: Atualiza automaticamente a interface

**Diretivas:**
- `v-if`: Renderização condicional de elementos
- `v-else`: Alternativa para renderização
- `v-for`: Loop para criar partículas
- `@click`: Event listener para cliques

**Binding:**
- `:class="{ quebrado: mensagemRevelada }"`: Classes condicionais
- `:style="{ ... }"`: Estilos dinâmicos
- `{{ mensagemAtual }}`: Interpolação de texto

## 🎨 Recursos Visuais

### Gradientes e Cores
- **Fundo:** Gradiente azul-roxo (`#667eea` → `#764ba2`)
- **Biscoito:** Gradiente dourado (`#f4d03f` → `#d4ac0d`)
- **Botão:** Gradiente laranja-vermelho (`#ff6b6b` → `#ee5a24`)

### Efeitos Visuais
- **Glassmorphism:** Fundo translúcido com blur na mensagem
- **Drop Shadow:** Sombras suaves nos elementos
- **Backdrop Filter:** Efeito de desfoque no fundo
- **Transform 3D:** Rotações e escalas em 3D

### Responsividade
```css
@media (max-width: 768px) {
    h1 { font-size: 2rem; }
    .biscoito { width: 150px; height: 150px; }
    .mensagem { font-size: 1rem; padding: 1rem 1.5rem; }
}
```

## 📱 Compatibilidade

- ✅ **Chrome** (versão 60+)
- ✅ **Firefox** (versão 55+)
- ✅ **Safari** (versão 12+)
- ✅ **Edge** (versão 79+)
- ✅ **Mobile** (iOS Safari, Chrome Mobile)

## 🎯 Funcionalidades

### Principais
- [x] Clique para quebrar o biscoito
- [x] 25 mensagens únicas de sorte
- [x] Animações suaves e fluidas
- [x] Design responsivo
- [x] Efeitos visuais modernos

### Interações
- [x] Hover effects no biscoito
- [x] Transições de estado
- [x] Feedback visual imediato
- [x] Botão para nova sorte

## 🔮 Mensagens de Sorte

O sistema inclui 25 mensagens motivacionais em português, cobrindo temas como:
- Amor e relacionamentos
- Sucesso profissional
- Crescimento pessoal
- Família e amizade
- Oportunidades futuras

## 🚀 Possíveis Melhorias

### Funcionalidades Futuras
- [ ] Sistema de favoritos para mensagens
- [ ] Compartilhamento nas redes sociais
- [ ] Histórico de mensagens recebidas
- [ ] Temas personalizáveis
- [ ] Sons de quebra do biscoito
- [ ] Animações mais elaboradas

### Melhorias Técnicas
- [ ] Service Worker para funcionamento offline
- [ ] Lazy loading de recursos
- [ ] Otimização de performance
- [ ] Testes automatizados
- [ ] TypeScript para maior robustez

## 🎉 Como Contribuir

1. **Fork** o projeto
2. **Crie** uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. **Commit** suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. **Push** para a branch (`git push origin feature/nova-feature`)
5. **Abra** um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar, modificar e distribuir.

## 👨‍💻 Autor

Criado com ❤️ usando Vue.js

---

**Divirta-se descobrindo sua sorte!** 🥠✨