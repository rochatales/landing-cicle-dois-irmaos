# Mapa de motion — LP Cicle Dois Irmãos

Tokens (em `:root`): `--ease: cubic-bezier(.22,1,.36,1)` · `--fast: .18s` · `--med: .35s` · `--slow: .7s`
Tudo é desligado com `prefers-reduced-motion: reduce` (transições, animações e reveal).

## Scroll
| Onde | Comportamento |
|---|---|
| `html` | `scroll-behavior: smooth` + `scroll-padding-top: 76px` (compensa o header fixo) |
| Todo `[id]` | `scroll-margin-top: 76px` — âncoras `#baixar`, `#baixar-2`, `#loja` param abaixo do header |
| Header `.top` | ganha sombra e encolhe (`.scrolled`) após 24px de rolagem |
| Reveal `[data-reveal]` | IntersectionObserver (threshold 8%, rootMargin -8%): fade + translateY(22px→0) em `--slow`, stagger de 70ms por irmão (`--i`). Só ativa com JS (`html.js`); sem JS tudo nasce visível. Hero nunca usa reveal. |
| CTA fixo mobile `.sticky` | entra/sai com `--ease` quando nenhum formulário está na tela |

Grupos com reveal: kicker/h2/lead de cada seção · 3 cards "jeitos de se mover" · 3 números (1967/2017/RETÜL) · capítulos · perfis · 4 itens Mantiqueira · destinos · serviços da loja · card Nero 6 · card da loja · CTA final · FAQ · colunas do rodapé.

## Empilhamento "wallet card" (GSAP ScrollTrigger 3.12.5, via cdnjs)
Referência: codepen.io/GreenSock/pen/bGRdvMy. Cada seção a partir de "problema" (problema → FAQ) vira um cartão; a hero fica de fora e rola normal, com a seção "problema" deslizando por cima dela: fica presa (pin) enquanto a seção seguinte desliza por cima, encolhendo para 85% e esmaecendo até 50%, depois some. O rodapé é o último cartão e não é coberto.

| Regra | Detalhe |
|---|---|
| Início do pin | Seção mais alta que a janela: quando a base encosta na base da janela (`bottom bottom`) — o conteúdo rola normal antes. Seção mais baixa: quando o topo encosta no topo (`top top`). |
| Fim do pin | Quando o topo da próxima seção chega ao topo da janela (`endTrigger: next, end: "top top"`). |
| `pinSpacing: false` | A página não ganha altura extra; as âncoras continuam nas posições naturais. |
| Âncoras e formulário | Como a seção presa fica `position: fixed`, a rolagem para `#baixar`, `#baixar-2`, erros do formulário e o bloco de obrigado usa a posição do `.pin-spacer` (função `scrollToEl`). |
| Sem GSAP / reduced-motion | A classe `html.stack` não é aplicada e a página rola normal, com as seções sobrepostas como antes. |

## Entrada (load)
| Elemento | Animação |
|---|---|
| `.hero .panel` | `panelIn` — fade + translateY(16px), .7s |
| `.hero .cover` | `coverIn` — fade + rotação -3°→1.6° + translateY(24px), .9s, delay .15s |

## Hover
| Elemento | Efeito |
|---|---|
| `.btn` (todos os CTAs) | sobe 2px + sombra; seta desliza 5px para a direita; `:active` comprime (.98) |
| `.btn.light` (header) | sombra |
| Logo no header | scale 1.05 |
| WhatsApp no header | fundo translúcido (sem animação no ícone) |
| Capa do e-book `.cover` | endireita (rotate 0), sobe 6px, scale 1.02, sombra maior |
| Inputs `.field input` | borda cinza no hover; no focus borda preta + sombra |
| Chips de interesse `.chip` | borda preta + sobe 1px; `:active` comprime |
| Checks do hero / serviços da loja | linha desliza 4px; círculo `.dot` cresce e gira -8° |
| Perguntas `.qs span` | fundo vermelho + texto branco + sobe 2px |
| Cards `.way` | borda superior vira vermelha; ilustração do veículo "anda" 10px; motor/raio vermelho cresce 18% |
| Números `.num` | borda superior vermelha; número desliza 4px |
| Selo "Em 2027, 60 anos" | raio pulsa a cada 2,6s (ambiente, não hover) |
| Capítulos `.chap li` | desliza 4px; numeral cresce 10% |
| Perfis `.for3 div` | sobe 4px + sombra; ícone cresce 15% |
| Itens Mantiqueira `.exp-item` | borda vermelha; ícone sobe 4px e cresce |
| Destinos `.places span` | fundo preto + texto branco + sobe 2px |
| Card Nero 6 `.pick` | ilustração anda 8px; specs ficam vermelhas |
| Card da loja `.where` | sobe 4px + sombra |
| FAQ `details` | sombra; o "+" gira 90° no hover e 45° (vira ×) ao abrir; resposta entra com fade |
| Redes sociais `.soc a` | sobe 3px |
